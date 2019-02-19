---
title: Inventário de software
titleSuffix: Configuration Manager
description: Veja uma introdução ao inventário de software no System Center Configuration Manager.
ms.date: 2/22/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 79eb49da-cd2b-4ffc-b355-b595aeba3aea
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 54bcd177d228e67748f561be556ff4219523711a
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56130404"
---
# <a name="introduction-to-software-inventory-in-system-center-configuration-manager"></a>Introdução ao inventário de software no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Use o inventário de software para coletar informações sobre arquivos em dispositivos cliente. O inventário de software também pode coletar arquivos de dispositivos cliente e armazená-los no servidor do site. O inventário de software é coletado quando você escolhe a configuração **Habilitar inventário de software em clientes** nas configurações do cliente, em que também é possível agendar a operação.  

Depois que o inventário de software é habilitado e os clientes executam um ciclo de inventário de software, o cliente envia as informações para um ponto de gerenciamento no site do cliente. Em seguida, o ponto de gerenciamento encaminha as informações de inventário para o servidor do site do Configuration Manager, que armazena as informações no banco de dados do site.   

 Aqui estão algumas maneiras para exibir os dados de inventário de software:  

- [Criar consultas](../../../../core/servers/manage/queries-technical-reference.md) que retornam dispositivos com arquivos especificados.   

- Criar [coleções com base em consulta](../../../../core/clients/manage/collections/introduction-to-collections.md) que incluem dispositivos com arquivos especificados.   

- [Executar relatórios](../../../../core/servers/manage/reporting.md) que fornecem detalhes sobre arquivos nos dispositivos.

- Use o [Gerenciador de Recursos](../../../../core/clients/manage/inventory/use-resource-explorer-to-view-software-inventory.md) para examinar informações detalhadas sobre os arquivos que foram inventariados e coletados dos dispositivos cliente.   

  Quando o inventário de software é executado em um dispositivo cliente, o primeiro relatório é um inventário completo. Os relatórios posteriores contêm apenas informações de delta de inventário. O servidor do site processa as informações de delta na ordem em que são recebidas. Se as informações de delta de um cliente estiverem ausentes, o servidor do site rejeitará as informações de delta adicionais e instruirá o cliente a executar um inventário completo.  

  O Configuration Manager pode descobrir computadores com inicialização dupla, mas só retorna informações de inventário do sistema operacional que estava ativo no momento do inventário.  

**Dispositivos móveis:** confira [Inventário de software para dispositivos móveis registrados com o Microsoft Intune](../../../../mdm/deploy-use/software-inventory-mobile-devices.md) para saber mais sobre a coleta de inventário para aplicativos instalados em dispositivos móveis.
