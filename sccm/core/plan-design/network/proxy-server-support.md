---
title: Suporte do servidor proxy
titleSuffix: Configuration Manager
description: Saiba como os servidores de sistemas de site do Configuration Manager usam servidores proxy.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 9123a87a-0b6f-43c7-b5c2-fac5d09686b1
author: mestew
ms.author: mstewart
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: e5c689ff3621477aa84d958e97c2dfebb81dcca1
ms.sourcegitcommit: 80cbc122937e1add82310b956f7b24296b9c8081
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/09/2019
ms.locfileid: "65499162"
---
# <a name="proxy-server-support-in-configuration-manager"></a>Suporte para servidor proxy no Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Alguns servidores de sistema de sites do Configuration Manager exigem conexão com a Internet. Se seu ambiente exigir tráfego da Internet para usar um servidor proxy, configure as funções desse sistema de sites para usar o proxy.  

-   Um computador que hospeda um servidor de sistema de sites dá suporte a uma única configuração de servidor proxy. Todas as funções do sistema de sites nesse computador compartilham essa mesma configuração de proxy. Se você precisar de servidores proxy separados para diferentes funções ou instâncias de uma função, coloque essas funções em servidores de sistemas de sites separados.  

-   Quando você define novas configurações de servidor proxy para um servidor de sistema de sites que já tem uma configuração de servidor proxy, a configuração original é substituída.  

-   Por padrão, as conexões com o proxy usam a conta **Sistema** do computador que hospeda a função de sistema de sites.  

-   Se a conta de computador não puder ser autenticada, o servidor do sistema de sites poderá armazenar as credenciais do usuário para conectar-se ao servidor proxy. Essas credenciais são a **conta do servidor proxy do sistema de sites**.  



## <a name="site-system-roles-that-use-a-proxy"></a>Funções do sistema de sites que usam um proxy

As seguintes funções do sistema de sites conectam-se à Internet e, se necessário, podem usar um servidor proxy:  


#### <a name="asset-intelligence-synchronization-point"></a>Ponto de sincronização do Asset Intelligence
Essa função do sistema de sites conecta-se à Microsoft e usa uma configuração de servidor proxy no computador que hospeda o ponto de sincronização do Asset Intelligence.  


#### <a name="cloud-distribution-point"></a>Ponto de distribuição na nuvem
A função do ponto de distribuição na nuvem é executada no Microsoft Azure. Não é necessário configurar essa função do sistema de sites para usar um proxy. Defina a configuração de proxy no servidor do site primário que gerencia o ponto de distribuição na nuvem.  

Para essa configuração, o servidor do site primário:  

-   Precisa ser capaz de se conectar ao Microsoft Azure para configurar, monitorar e distribuir conteúdo ao ponto de distribuição na nuvem.  

-   Por padrão, usa a conta **Sistema** do computador para fazer a conexão. Ele também pode usar a conta do servidor proxy do sistema de sites, se necessário.  

-   Usa as APIs do navegador da Web do Windows.  


#### <a name="exchange-server-connector"></a>Conector do Exchange Server
Essa função do sistema de sites conecta-se a um Exchange Server. Ela usa uma configuração de servidor proxy no computador que hospeda o conector do Exchange Server.  


#### <a name="service-connection-point"></a>Ponto de Conexão de Serviço
Essa função do sistema de sites conecta-se ao serviço de nuvem do Configuration Manager para baixar as atualizações de versão do Configuration Manager e conecta-se ao Microsoft Intune em uma configuração híbrida. Ela usa um servidor proxy que está configurado no computador que hospeda o ponto de conexão de serviço.  


#### <a name="software-update-point"></a>Ponto de atualização de software
Essa função do sistema de sites usa o proxy ao conectar-se com o Microsoft Update para baixar patches e sincronizar informações sobre atualizações. Como em qualquer outra função do sistema de sites, primeiro defina as configurações de proxy do sistema de sites. Em seguida, configure as seguintes opções específicas do ponto de atualização de software:  

-   **Usar um servidor proxy ao sincronizar atualizações de software**  

-   **Usar um servidor proxy ao baixar conteúdo usando as regras de implantação automática**  

    > [!Note]  
    > Embora esteja disponível para ser usada, essa configuração não é usada por pontos de atualização de software em sites secundários.  

Essas configurações ficam na guia **Configurações de Proxy e Conta** das propriedades do ponto de atualização de software.  

> [!NOTE]  
>  Por padrão, quando as regras de implantação automática são executadas, a conta do **Sistema** no servidor de sites do site no qual uma regra de implantação automática foi criada é usada para conectar-se à Internet e baixar atualizações do software. Como alternativa, configure e use a conta do servidor proxy do sistema de sites. 
>   
>  Quando essa conta não pode acessar a Internet, não é possível baixar as atualizações de software. A seguinte entrada é registrada em **ruleengine.log**:  
> `Failed to download the update from internet. Error = 12007.`  



## <a name="configure-the-proxy-for-a-site-system-server"></a>Configurar o proxy para um servidor do sistema de sites  

1.  No console do Configuration Manager, acesse o workspace **Administração**. Expanda **Configuração do Site** e, em seguida, selecione o nó **Servidores e Funções do Sistema de Sites**.  

2.  Selecione o servidor do sistema de sites que você deseja editar. No painel de detalhes, clique com o botão direito do mouse na função **Sistema de sites** e selecione **Propriedades**.  

3.  Em Propriedades do sistema de sites, mude para a guia **Proxy**. Defina as seguintes configurações de proxy:  

    - **Usar um servidor proxy ao sincronizar informações da Internet**: selecione essa opção para permitir que o servidor do sistema de sites use um servidor proxy.  

    - **Nome do servidor proxy**: especifique o nome do host ou o FQDN do servidor proxy em seu ambiente.  

    - **Porta**: especifique a porta de rede que será usada para a comunicação com o servidor proxy. Por padrão, ele usa a porta **80**.  

    - **Use as credenciais para se conectar ao servidor proxy**: muitos servidores proxy exigem que um usuário se autentique. Por padrão, o servidor do sistema de sites usa sua conta de computador para conectar-se ao servidor proxy. Se necessário, habilite essa opção, clique em **Definir** e, em seguida, escolha uma **Conta Existente** ou especifique uma **Nova Conta**. Essas credenciais são a **conta do servidor proxy do sistema de sites**.  Para obter mais informações, confira [Contas usadas no Configuration Manager](/sccm/core/plan-design/hierarchy/accounts).  

4.  Clique em **OK** para salvar a nova configuração do servidor proxy.  
