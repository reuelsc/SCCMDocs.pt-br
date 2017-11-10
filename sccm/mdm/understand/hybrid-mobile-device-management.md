---
title: "Gerenciamento de dispositivo móvel (MDM ) híbrido com o Microsoft Intune"
titleSuffix: Configuration Manager
description: "Saiba mais sobre o MDM (gerenciamento de dispositivo móvel) híbrido com o System Center Configuration Manager e o Microsoft Intune."
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: bb95154b-f63e-4491-896e-41d732c802f8
caps.latest.revision: "34"
caps.handback.revision: "0"
author: dougeby
ms.author: dougeby
manager: angrobe
ms.openlocfilehash: da817ac299115c1151851d302c1935ad3f956bdf
ms.sourcegitcommit: c236214b2fcc13dae7bad96d7fb33f692868191d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2017
---
# <a name="hybrid-mobile-device-management-mdm-with-system-center-configuration-manager-and-microsoft-intune"></a>MDM (gerenciamento de dispositivo móvel) híbrido com o System Center Configuration Manager e o Microsoft Intune

*Aplica-se a: System Center Configuration Manager (Branch Atual)*


É possível gerenciar dispositivos iOS, Windows e Android com o Configuration Manager e o Microsoft Intune. Todas as tarefas de gerenciamento são tratadas no console do Configuration Manager, em que você executa o restante de suas tarefas de gerenciamento de forma diretamente integrada ao serviço online do Microsoft Intune pela Internet.  É possível usar o Configuration Manager para permitir que os usuários acessem recursos da empresa em seus dispositivos de maneira segura e gerenciada. Usando o gerenciamento de dispositivos, você protege os dados da empresa enquanto permite que os usuários registrem dispositivos pessoais ou da empresa para acessar dados da empresa. Recursos de gerenciamento dos dispositivos:

-   Desativar e apagar dispositivos
-   Definir configurações de conformidade, como senhas, segurança, roaming, criptografia e comunicação sem fio
-   Implantar aplicativos de LOB (linha de negócios) em dispositivos
-   Implantar aplicativos em dispositivos que se conectam à Windows Store, Windows Phone Store, App Store ou Google Play
-   Coletar inventário de hardware
-   Coletar inventário de software usando relatórios internos

Para ler sobre os novos recursos que estão disponíveis para o MDM híbrido, consulte [What's new in hybrid mobile device management](../understand/whats-new-in-hybrid-mobile-device-management.md) (O que há de novo no gerenciamento de dispositivo móvel híbrido).

Este documento pressupõe que você esteja usando o Configuration Manager para gerenciar computadores, e que esteja interessado em estender o console do Configuration Manager com o Intune para gerenciar dispositivos móveis. Para entender as diferenças entre o Intune e gerenciamento de dispositivos móveis híbrido, consulte [Escolha entre o gerenciamento de dispositivo móvel híbrido e independente do Microsoft Intune com o System Center Configuration Manager](choose-between-standalone-intune-and-hybrid-mobile-device-management.md).

Após estender o Configuration Manager com o Intune, você pode registrar e gerenciar dispositivos corporativos ou conceder aos usuários permissão para registrar seus dispositivos pessoais. Você também pode gerenciar dispositivos corporativos com o Intune usando o Configuration Manager.

## <a name="hybrid-mdm-enrollment"></a>Registro no MDM híbrido
Para colocar dispositivos no gerenciamento híbrido, esses dispositivos devem estar registrados no serviço. A forma como os dispositivos são registrados depende do tipo de dispositivo, da propriedade e do nível de gerenciamento necessário.
- O registro de BYOD ("Traga seu próprio dispositivo") permite que os usuários registrem telefones, tablets ou PCs pessoais.
- O registro de COD (dispositivo corporativo) permite cenários de gerenciamento como apagamento remoto, dispositivos compartilhados ou afinidade de usuário para um dispositivo.
- Se usar o [Exchange ActiveSync](../plan-design/device-enrollment-methods.md#mobile-device-management-with-exchange-activesync-and-configuration-manager), seja localmente ou hospedado na nuvem, você poderá habilitar o gerenciamento simples do Intune sem o registro. Computadores Windows também podem ser gerenciados usando o [Software cliente do Intune](/intune/deploy-use/manage-windows-pcs-with-microsoft-intune).
