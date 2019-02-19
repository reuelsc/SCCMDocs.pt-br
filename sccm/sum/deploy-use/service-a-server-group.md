---
title: Realização de serviços em um grupo de servidores
titleSuffix: Configuration Manager
description: O console do System Center Configuration Manager fornece alertas e status para monitorar atualizações e a conformidade.
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 12/07/2016
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: 304a83ea-0f72-437d-9688-2e6e0c7526dd
ms.collection: M365-identity-device-management
ms.openlocfilehash: aac5c9d6c683447fe7dda50e6dcfd52b7024656d
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56131635"
---
# <a name="service-a-server-group"></a>Realização de serviços em um grupo de servidores

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

>[!IMPORTANT]
>Os recursos de pré-lançamento são recursos que estão na Ramificação atual para testes iniciais em um ambiente de produção. Esses recursos têm suporte total, mas ainda estão em desenvolvimento ativo e podem receber alterações até que saiam da categoria de pré-lançamento. Você deve ativar esse recurso para que ele seja disponibilizado. Para obter mais informações, consulte [Usar recursos de pré-lançamento de atualizações](https://docs.microsoft.com/sccm/core/servers/manage/install-in-console-updates#bkmk_prerelease).

A partir do System Center Configuration Manager versão 1606, é possível definir configurações de grupo de servidores para uma coleção para definir quantos, qual percentual ou em que ordem os computadores da coleção instalarão as atualizações de software. Também é possível configurar scripts pré-implantação e pós-implantação do PowerShell para executar ações personalizadas.

Quando você implanta atualizações de software em uma coleção que tem configurações de grupo de servidores definidas, o Configuration Manager determina quantos computadores da coleção podem instalar as atualizações de software a qualquer dado momento e disponibiliza o mesmo número de bloqueios de implantação. Somente computadores que receberem um bloqueio de implantação iniciarão a instalação da atualização de software. Quando um bloqueio de implantação está disponível, um computador obtém o bloqueio de implantação, instala as atualizações de software e libera o bloqueio de implantação quando a instalação das atualizações de software é concluída com êxito. Depois, o bloqueio de implantação fica disponível para outros computadores. Quando um computador não consegue liberar um bloqueio de implantação, você pode liberar manualmente todos os bloqueios de implantação do grupo de servidores para a coleção.

>[!IMPORTANT]
>Todos os computadores da coleção devem ser atribuídos ao mesmo site.

#### <a name="to-create-a-collection-for-a-server-group"></a>Para criar uma coleção para um grupo de servidores  
As configurações do grupo do servidores são definidas nas propriedades de uma coleção de dispositivos. Para realizar serviços em um grupo de servidores, todos os membros da coleção devem ser atribuídos ao mesmo site. Use as etapas a seguir para criar uma coleção e definir as configurações do grupo de servidores:
1.  [Crie uma coleção de dispositivos](../../core/clients/manage/collections/create-collections.md) que contém os computadores do grupo de servidores.  

2.  No workspace **Ativos e Conformidade**, clique em **Coleções de Dispositivos**, clique com o botão direito do mouse na coleção que contém os computadores do grupo de servidores e clique em **Propriedades**.  

3.  Na guia **Geral**, selecione **Todos os dispositivos fazem parte do mesmo grupo de servidores** e clique em **Configurações**.  

4.  Na página **Configurações do Grupo de Servidor**, especifique uma das seguintes configurações:  

    -   **Permitir que um percentual dos computadores seja atualizado ao mesmo tempo**: Especifica que apenas um determinado percentual de clientes seja atualizado a qualquer momento. Se, por exemplo, a coleção tiver 10 clientes e for configurada para atualizar 30% dos clientes ao mesmo tempo, apenas três clientes instalarão atualizações de software a qualquer momento.  

    -   **Permitir que vários computadores sejam atualizados ao mesmo tempo**: Especifica que apenas um determinado número de clientes seja atualizado a qualquer momento.  

    -   **Especificar a sequência de manutenção**: especifica que os clientes na coleção serão atualizados um de cada vez na sequência que você configurar. Um cliente instalará atualizações de software apenas depois que o cliente que está à sua frente na lista terminar de instalar atualizações de software.  

5.  Especifique se deseja usar um script de pré-implantação (drenagem de nó) ou pós-implantação (retomada de nó).  

    > [!WARNING]
    > Scripts personalizados não são assinados pela Microsoft. É sua responsabilidade manter a integridade desses scripts.

    > [!TIP]  
    > Veja abaixo exemplos que você pode usar em testes de scripts de pré-implantação e pós-implantação que gravam a hora atual em um arquivo de texto:  
    >   
    >  **Pré-implantação**  
    >   
    >  `#Start`  
    >   
    >  `$a = Get-Date`  
    >   
    >  `Write-Output "Universal Time: " + $a.ToUniversalTime()  |`  
    >   
    >  `Out-File C:\Windows\Temp\start.txt`  
    >   
    >  **Pós-implantação**  
    >   
    >  `#End`  
    >   
    >  `$a = Get-Date`  
    >   
    >  `Write-Output "Universal Time: " + $a.ToUniversalTime()  |`  
    >   
    >  `Out-File C:\Windows\Temp\end.txt`  

## <a name="deploy-software-updates-to-the-server-group-and-monitor-status"></a>Implantar atualizações de software no grupo de servidores e monitorar o status  
Implante atualizações de software na coleção do grupo de servidores usando o processo típico de implantação. Após implantar as atualizações de software, você pode monitorar a implantação da atualização de software no console do Configuration Manager.
1.  [Implante atualizações de software](manually-deploy-software-updates.md) na coleção do grupo de servidores.   

2.  [Monitore a implantação de atualização de software](monitor-software-updates.md). Além dos modos de exibição de monitoramento padrão para a implantação de atualizações de software, o estado **Aguardando o bloqueio** é exibido quando um cliente está esperando sua vez para instalar as atualizações de software. Examine o arquivo UpdatesDeployment.log para obter mais informações.


## <a name="clear-the-deployment-locks-for-computers-in-a-server-group"></a>Limpe os bloqueios de implantação para computadores em um grupo de servidores  
Quando um computador falha ao liberar um bloqueio de implantação, você pode liberar manualmente todos os bloqueios de implantação do grupo de servidores para a coleção. Limpe os bloqueios somente quando uma implantação ficar presa atualizando computadores da coleção e houver computadores que ainda não são compatíveis.  
1.  No workspace **Ativos e Conformidade**, clique em **Coleções de Dispositivos** e clique na coleção para limpar os bloqueios de implantação.  

2.  Na guia **Início**, no grupo **Implantação**, clique em **Limpar Bloqueios de Implantação de Grupo de Servidores**. Quando os clientes não conseguem instalar as atualizações de software e impedem que outros clientes instale suas atualizações de software, os bloqueios de implantação podem ser removidos manualmente.  
