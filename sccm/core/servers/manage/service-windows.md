---
title: "Períodos de manutenção | Microsoft Docs"
description: "Use períodos de manutenção para controlar quando os sites do System Center Configuration Manager instalam atualizações."
ms.custom: na
ms.date: 1/11/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ca4886d4-7173-46be-8dcd-1657d5b0deb9
caps.latest.revision: "4"
caps.handback.revision: "0"
author: Dougeby
ms.author: dougeby
manager: angrobe
ms.openlocfilehash: d06a2a955ff59fa84bb844033fe31874fc735087
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/07/2017
---
#  <a name="service-windows-for-site-servers"></a>Períodos de manutenção para servidores de site

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Você pode configurar períodos de manutenção em sites de administração central e em sites primários a fim de controlar quando as atualizações no console podem ser instaladas.  É possível configurar vários períodos, com o período permitido para instalação de atualizações determinado por uma combinação de todos os períodos de serviço para esse servidor do site.

Quando não houver um nenhum período de manutenção configurado:
- **Em seu site de nível superior** (um site de administração central ou um site primário autônomo) escolha quando iniciar a instalação da atualização.
- **Em um site primário filho**, a atualização é instalada automaticamente após a conclusão da atualização no site de administração central.
- **Em um site secundário**, as atualizações nunca começam automaticamente. Em vez disso, você deve iniciar manualmente a atualização da instalação de dentro do console, após a instalação da atualização pelo site pai primário.

Quando houver um período de manutenção configurado:
- **Em seu site de nível superior**, você não poderá iniciar a instalação de qualquer atualização nova do console do Configuration Manager. Mesmo com um período de serviço configurado, o site baixa atualizações automaticamente para que estejam prontas instalação.  
- **Em um site primário filho**, as atualizações instaladas em um site de administração central serão baixadas no site primário, mas não começarão automaticamente. Você não pode iniciar manualmente a instalação de uma atualização durante um período bloqueado pelo uso de um período de manutenção. Quando o período de manutenção não bloquear mais a instalação da atualização, a atualização instalada será iniciada automaticamente.
- **Sites secundários** não oferecem suporte a períodos de manutenção, e não instalam atualizações automaticamente. Após um site primário pai de um site secundário instalar uma atualização, você poderá iniciar a atualização do site secundário a partir do console.

## <a name="to-configure-a-service-window"></a>Para configurar um período de manutenção

1.  No console do Configuration Manager, abra **Administração** > **Configuração de Site** > **Sites** e selecione o servidor do site para o qual deseja configurar um período de serviço.  

2.  Em seguida, edite as **Propriedades** dos servidores do site e selecione a guia **Período de Serviço** , na qual você pode definir um ou mais períodos de serviço para o servidor do site.  
