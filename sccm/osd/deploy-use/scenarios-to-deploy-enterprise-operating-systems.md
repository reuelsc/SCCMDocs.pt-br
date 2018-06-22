---
title: Cenários para implantar sistemas operacionais corporativos
titleSuffix: Configuration Manager
description: Conheça vários cenários para implantar sistemas operacionais corporativos com o System Center Configuration Manager.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: f74fdb86-c7c2-447f-91f6-b42df6370d7f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: d0beb10dca04fe26fb4add22b64ab61b53154185
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32349160"
---
# <a name="scenarios-to-deploy-enterprise-operating-systems-with-system-center-configuration-manager"></a>Cenários para implantar sistemas operacionais corporativos com o System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Os seguintes cenários de implantação de sistema operacional estão disponíveis no System Center Configuration Manager:  

-   [Atualizar o Windows para a versão mais recente](upgrade-windows-to-the-latest-version.md): esse cenário atualiza o sistema operacional em computadores que atualmente executam o Windows 7, Windows 8, Windows 8.1 ou Windows 10. O processo de atualização mantém os aplicativos, as configurações e os dados do usuário no computador. Não há dependências externas, como o Windows ADK, e esse processo é mais rápido e mais resiliente do que as implantações tradicionais de sistema operacional.  

-   [Atualizar um computador existente com uma nova versão do Windows usando o System Center Configuration Manager](refresh-an-existing-computer-with-a-new-version-of-windows.md): esse cenário particiona e formata (apaga) um computador existente e instala um novo sistema operacional no computador. É possível migrar configurações e dados do usuário após a instalação do sistema operacional.  

-   [Instalar uma nova versão do Windows em um novo computador (sem sistema operacional) com o System Center Configuration Manager](install-new-windows-version-new-computer-bare-metal.md): esse cenário instala um sistema operacional em um novo computador. Essa é uma nova instalação do sistema operacional e não inclui nenhuma configuração ou migração de dados do usuário.  

-   [Substituir um computador existente e transferir configurações com o System Center Configuration Manager](replace-an-existing-computer-and-transfer-settings.md): esse cenário instala um sistema operacional em um novo computador. Opcionalmente, é possível migrar configurações e dados do usuário do computador antigo para o novo.  

## <a name="things-to-consider-before-you-deploy-operating-system-images"></a>Coisas a considerar antes de implantar imagens do sistema operacional  
 Existem certas coisas que você deve considerar antes de implantar um sistema operacional.  

### <a name="operating-system-image-size"></a>Tamanho da imagem do sistema operacional  
 O tamanho da imagem de um sistema operacional pode ser bem grande. Por exemplo, o tamanho da imagem do Windows 7 é de 3 GB ou mais. O tamanho da imagem e o número de computadores em que o sistema operacional é implantado simultaneamente afeta o desempenho da rede e a largura de banda disponível. Lembre-se de testar o desempenho da rede para avaliar melhor o possível impacto da implantação da imagem e o tempo necessário para concluir a implantação. As atividades do Configuration Manager que afetam o desempenho da rede estão a distribuição da imagem para um ponto de distribuição, distribuição da imagem de um site para outro e download da imagem para o cliente do Configuration Manager.  

 Também é preciso planejar espaço de armazenamento em disco suficiente nos pontos de distribuição que hospedam as imagens do sistema operacional.  

### <a name="client-cache-size"></a>Tamanho do cache do cliente  
 Quando os clientes do Configuration Manager baixam conteúdo, eles usam automaticamente o BITS (Serviço de Transferência Inteligente em Segundo Plano), se disponível. Ao implantar uma sequência de tarefas que instala um sistema operacional, é possível definir uma opção na implantação para que os clientes do Configuration Manager baixem a imagem completa em um cache local antes que a sequência de tarefas seja executada.  

 Em geral, quando um cliente do Configuration Manager precisa baixar a imagem de um sistema operacional (ou qualquer outro pacote), mas não há espaço suficiente no cache, o cliente verifica os outros pacotes no cache para determinar se a exclusão de algum ou de todos os pacotes mais antigos liberará espaço em disco suficiente para acomodar a imagem. Se excluir pacotes não liberar espaço em disco suficiente, o cliente não baixa a nova imagem e a implantação falha. Isso pode ocorrer se o cache tiver um pacote grande configurado para persistir no cache. Se excluir pacotes liberar espaço suficiente no cache, o cliente os exclui e depois baixa o novo pacote no cache.  

 O tamanho padrão do cache em clientes do Configuration Manager pode não ser suficientemente grande para a maioria das implantações de imagem do sistema operacional. Se você planeja baixar a imagem completa no cache do cliente, ajuste o tamanho do cache do cliente do Configuration Manager nos computadores de destino para acomodar o tamanho da imagem que será implantada.  

 Para obter mais informações, consulte [Configurar o cache de cliente para clientes do Configuration Manager](../../core/clients/manage/manage-clients.md#BKMK_ClientCache).  

## <a name="task-sequence-deployments"></a>Implantações de sequência de tarefas  
 A sequência de tarefas criada pode implantar a imagem do sistema operacional em um computador cliente do Configuration Manager de uma das seguintes maneiras:  

-   Baixar a imagem e seu conteúdo primeiramente no cache do cliente do Configuration Manager de um ponto de distribuição e instalá-la.  

-   Instalar a imagem e seu conteúdo diretamente do ponto de distribuição.  

-   Instalar a imagem e seu conteúdo conforme necessário a partir do ponto de distribuição.  

 Por padrão, ao criar a implantação de uma sequência de tarefas, a imagem é baixada primeiramente no cache do cliente do Configuration Manager e instalada em seguida. Se você optar por baixar a imagem no cache do cliente do Configuration Manager antes de executá-la, e a sequência de tarefas contiver uma etapa para reparticionar o disco rígido, a etapa de reparticionamento falhará, pois particionar o disco rígido apagará o conteúdo do cache do cliente do Configuration Manager. Se a sequência de tarefas precisar reparticionar o disco rígido, será necessário executar a instalação da imagem no ponto de distribuição usando a opção **Executar programa do ponto de distribuição**  ao implantar a sequência de tarefas.  

 Para obter mais informações, consulte [Deploy a task sequence](manage-task-sequences-to-automate-tasks.md#BKMK_DeployTS).  
