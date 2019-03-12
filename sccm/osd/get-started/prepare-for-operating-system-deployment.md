---
title: Preparar a implantação do sistema operacional
titleSuffix: Configuration Manager
description: Saiba como preparar implantações de sistema operacional no Configuration Manager
ms.date: 02/22/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 8d27e5ac-4f19-4b3d-85c7-fa34eb5d5e7e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 7e303a7363e0641210cc7c6e436546d864fe0571
ms.sourcegitcommit: ef2960bd91655c741450774e512dd0a9be610625
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 02/26/2019
ms.locfileid: "56838711"
---
# <a name="prepare-for-os-deployment-in-configuration-manager"></a>Preparar a implantação do sistema operacional no Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Há várias coisas que você deve fazer no Configuration Manager antes de poder implantar sistemas operacionais. Leia os seguintes artigos para se preparar para a implantação do sistema operacional:  

-   [Gerenciar imagens de inicialização](manage-boot-images.md)  

-   [Gerenciar imagens do sistema operacional](manage-operating-system-images.md)  

-   [Gerenciar pacotes de atualização do sistema operacional](manage-operating-system-upgrade-packages.md)  

-   [Gerenciar drivers](manage-drivers.md)  

-   [Gerenciar o estado do usuário](manage-user-state.md)  

-   [Preparar-se para implantações em computadores desconhecidos](prepare-for-unknown-computer-deployments.md)  

-   [Associar usuários a um computador de destino](associate-users-with-a-destination-computer.md)  



### <a name="os-image-size"></a>Tamanho da imagem do sistema operacional  

As imagens do sistema operacional são grandes. Por exemplo, o tamanho da imagem do Windows 7 é 3 GB ou mais. O tamanho da imagem e o número de computadores em que o sistema operacional é implantado simultaneamente afeta o desempenho da rede e a largura de banda disponível. Teste o desempenho da rede. Testar o impacto estimará melhor o efeito que a implantação da imagem poderá ter e o tempo necessário para concluir a implantação. As atividades do Configuration Manager que afetam o desempenho da rede incluem a distribuição da imagem para um ponto de distribuição, a distribuição da imagem de um site para outro e o download da imagem no cliente.  

Também é preciso planejar o espaço suficiente de armazenamento em disco nos pontos de distribuição que hospedam as imagens do sistema operacional.  

Para saber mais, confira as [considerações de planejamento adicionais para os pontos de distribuição](/sccm/osd/get-started/prepare-site-system-roles-for-operating-system-deployments#BKMK_AdditionalPlanning).


### <a name="client-cache-size"></a>Tamanho do cache do cliente  

Quando os clientes do Configuration Manager baixam conteúdo, eles usam automaticamente o BITS (Serviço de Transferência Inteligente em Segundo Plano), se estiver disponível. Ao implantar uma sequência de tarefas que instala um sistema operacional, é possível definir uma opção na implantação para que os clientes do Configuration Manager baixem a imagem completa em um cache local antes que a sequência de tarefas seja executada.  

Quando um cliente do Configuration Manager precisa baixar uma imagem do sistema operacional, mas não há espaço suficiente no cache, o cliente pode limpar espaço em seu cache. Ele verifica os outros pacotes no cache para determinar se a exclusão de qualquer um dos pacotes mais antigos liberará espaço em disco suficiente para acomodar a imagem. Se excluir pacotes não liberar espaço suficiente em disco, o cliente não baixará a nova imagem, e a implantação falhará. Esse comportamento pode ocorrer se o cache tiver um pacote grande que você configura para persistir no cache. Se excluir pacotes liberar espaço suficiente no cache, o cliente os exclui e depois baixa o novo pacote no cache.  

O tamanho padrão do cache nos clientes do Configuration Manager pode não ser suficientemente grande para a maioria das implantações de imagem do sistema operacional. Se você planeja baixar a imagem completa no cache do cliente, ajuste o tamanho do cache do cliente nos computadores de destino para acomodar o tamanho da imagem que será implantada.  

Para saber mais, confira [Configurar o tamanho do cache do cliente](/sccm/core/clients/manage/manage-clients#BKMK_ClientCache).  


