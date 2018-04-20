---
title: Painel de dispositivos Surface
titleSuffix: System Center Configuration Manager
description: Examine as informações sobre os dispositivos Surface usando o painel.
keywords: ''
author: mestew
ms.author: mstewart
manager: dougeby
ms.date: 03/22/2018
ms.topic: article
ms.prod: configuration-manager
ms.service: ''
ms.technology:
- configmgr-other
ms.assetid: 7397fc17-3ae8-4525-8386-aea8a9cffa06
ms.openlocfilehash: 8c9171ed5b239091b7f77b534368422575c0f2f4
ms.sourcegitcommit: fb84bcb31d825f454785e3d9d8be669e00fe2b27
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
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
![Surface device dashboard](media\Surface-device-dashboard.PNG)



## <a name="reviewing-information-in-the-surface-device-dashboard"></a>Examinando informações no painel de dispositivos Surface

O painel de dispositivos Surface mostra três grafos para o ambiente. 

- **Percentual de dispositivos Surface** – fornece o percentual de dispositivos Surface em todo o ambiente.

    ![Grafo de percentual de dispositivos Surface](media\Percent-Surface-Devices.PNG)
- **Modelos Surface** – mostra o número de dispositivos por modelo Surface. 
    - Focalizar uma seção do grafo fornecerá o percentual de dispositivos Surface com o modelo selecionado. 

         ![Grafo de modelos Surface](media\Surface-Models-Hover.PNG)
    - Clicar em uma seção do grafo levará você a uma lista de dispositivos com o modelo. 
        ![Lista de dispositivos com o modelo Surface](media\Surface-Model-Device-List.PNG)

- **Cinco principais versões de firmware** – exibe um gráfico com os cinco principais modelos de firmware no ambiente. 
    - Focalizar uma seção do grafo fornecerá o número de dispositivos Surface com a versão de firmware selecionada. 
       ![Lista de dispositivos com o modelo Surface](media\Surface-Firmware-Hover.PNG)


## <a name="more-information"></a>Mais informações

Para obter mais informações sobre dispositivos Surface, consulte:
 - O site do [Surface]( https://go.microsoft.com/fwlink/?linkid=861998).
    
Para obter mais informações de como implantar atualizações de firmware do Surface no Configuration Manager, confira:
 - [Como gerenciar atualizações de driver do Surface no Configuration Manager]( https://support.microsoft.com/help/4098906).




