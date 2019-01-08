---
title: Painel de dispositivos Surface
titleSuffix: Configuration Manager
description: Examine as informações sobre os dispositivos Surface usando o painel.
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 07/30/2018
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.assetid: 7397fc17-3ae8-4525-8386-aea8a9cffa06
ms.openlocfilehash: b49a794a4036a3f2a8d42dc3b71855b44c22f44b
ms.sourcegitcommit: 48098f9fb2f447672bf36d50c9f58a3d26acb9ed
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2018
ms.locfileid: "53422599"
---
# <a name="surface-device-dashboard-in-system-center-configuration-manager"></a>Painel de dispositivos Surface no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

A partir da versão 1802, o painel de dispositivos Surface fornece rapidamente informações sobre os dispositivos Surface encontrados no ambiente. <!--1355788-->

## <a name="open-the-surface-device-dashboard"></a>Abrir o painel de dispositivos Surface

Para abrir o painel de dispositivos Surface, use as seguintes etapas: 

1. Abra o console do gerenciador de configurações. 
2. Clique no nó **Monitoramento**. 
3. Para carregar o painel, clique em **Dispositivos Surface**.

**Painel de dispositivos Surface**
![Surface device dashboard](media/Surface-device-dashboard.PNG)



## <a name="reviewing-information-in-the-surface-device-dashboard"></a>Examinando informações no painel de dispositivos Surface

O painel de dispositivos Surface mostra três grafos para o ambiente. 

- **Percentual de dispositivos Surface** – fornece o percentual de dispositivos Surface em todo o ambiente.

    ![Grafo de percentual de dispositivos Surface](media/Percent-Surface-Devices.PNG)
- **Modelos Surface** – mostra o número de dispositivos por modelo Surface. 
  - Focalizar uma seção do grafo fornecerá o percentual de dispositivos Surface com o modelo selecionado. 

       ![Grafo de modelos Surface](media/Surface-Models-Hover.PNG)
  - Clicar em uma seção do grafo levará você a uma lista de dispositivos com o modelo. 
      ![Lista de dispositivos com o modelo Surface](media/Surface-Model-Device-List.PNG)

- **Cinco principais versões de firmware** – exibe um gráfico com os cinco principais modelos de firmware no ambiente. 
  - Focalizar uma seção do grafo fornecerá o número de dispositivos Surface com a versão de firmware selecionada. Começando com o Configuration Manager versão 1806, quando você clica em uma seção do grafo, uma lista de dispositivos relevantes é exibida. <!--1358654--> ![Lista de dispositivos de modelo do Surface](media/Surface-Firmware-Hover.PNG)


## <a name="more-information"></a>Mais informações

Para obter mais informações sobre dispositivos Surface, consulte:
 - O site do [Surface]( https://go.microsoft.com/fwlink/?linkid=861998).
    
Para obter mais informações de como implantar atualizações de firmware do Surface no Configuration Manager, confira:
 - [Como gerenciar atualizações de driver do Surface no Configuration Manager]( https://support.microsoft.com/help/4098906).




