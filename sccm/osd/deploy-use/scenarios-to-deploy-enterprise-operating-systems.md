---
title: Cenários para implantar sistemas operacionais corporativos
titleSuffix: Configuration Manager
description: Conheça vários cenários para implantar sistemas operacionais corporativos com o Configuration Manager.
ms.date: 02/22/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: f74fdb86-c7c2-447f-91f6-b42df6370d7f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: f6d34c3d8dfa753934f03337d68e989a8bf8fcd7
ms.sourcegitcommit: ef2960bd91655c741450774e512dd0a9be610625
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 02/26/2019
ms.locfileid: "56838694"
---
# <a name="scenarios-to-deploy-enterprise-operating-systems-with-configuration-manager"></a>Cenários para implantar sistemas operacionais corporativos com o Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Os seguintes cenários de implantação de sistema operacional estão disponíveis no Configuration Manager:  

#### <a name="upgrade-windows-to-the-latest-version"></a>Atualizar o Windows para a última versão
Este cenário atualiza o sistema operacional em computadores que atualmente executam o Windows 7, Windows 8.1 ou o Windows 10. O processo de atualização mantém os aplicativos, as configurações e os dados do usuário no computador. Não há dependências externas, como o Windows ADK. Esse processo pode ser mais rápido e mais resiliente do que as implantações tradicionais de sistema operacional.  

Para obter mais informações, confira [Atualizar o Windows para a versão mais recente](/sccm/osd/deploy-use/upgrade-windows-to-the-latest-version).


#### <a name="windows-autopilot-for-existing-devices"></a>Windows Autopilot para dispositivos existentes
<!--3607717, fka 1358333--> A partir da versão 1810, o Windows Autopilot para dispositivos existentes está disponível com o Windows 10, versão 1809 ou posterior. Esse recurso permite refazer a imagem e provisionar um dispositivo Windows 7 para o modo orientado pelo usuário do Windows Autopilot usando uma única sequência de tarefas do Configuration Manager.

Para saber mais, confira [Windows Autopilot para dispositivos existentes](/sccm/osd/deploy-use/windows-autopilot-for-existing-devices).


#### <a name="refresh-an-existing-computer-with-a-new-version-of-windows"></a>Atualizar um computador existente com uma nova versão do Windows
Este cenário particiona e formata (apaga) um computador existente e instala um novo sistema operacional nele. É possível migrar as configurações e os dados do usuário após a instalação do sistema operacional.  

Para saber mais, confira [Atualizar um computador existente com uma nova versão do Windows](/sccm/osd/deploy-use/refresh-an-existing-computer-with-a-new-version-of-windows).


#### <a name="install-a-new-version-of-windows-on-a-new-computer-bare-metal"></a>Instalar uma nova versão do Windows em um novo computador (sem sistema operacional)
Este cenário instala um sistema operacional em um novo computador. Essa é uma nova instalação do sistema operacional e não inclui nenhuma configuração ou migração de dados do usuário.  

Para saber mais, confira [Instalar uma nova versão do Windows em um novo computador (sem sistema operacional)](/sccm/osd/deploy-use/install-new-windows-version-new-computer-bare-metal).


#### <a name="replace-an-existing-computer-and-transfer-settings"></a>Substituir um computador existente e transferir configurações
Este cenário instala um sistema operacional em um novo computador. Opcionalmente, é possível migrar configurações e dados do usuário do computador antigo para o novo.  

Para mais informações, consulte [Replace an existing computer and transfer settings (Substituir um computador existente e transferir configurações)](/sccm/osd/deploy-use/replace-an-existing-computer-and-transfer-settings).


