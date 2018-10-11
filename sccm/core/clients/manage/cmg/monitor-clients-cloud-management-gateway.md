---
title: Monitorar o gateway de gerenciamento de nuvem
titleSuffix: Configuration Manager
description: Monitore os clientes e o tráfego de rede por meio do CMG (gateway de gerenciamento de nuvem).
ms.date: 09/10/2018
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 15f72f80-9850-40ce-9c3a-443ba04b6a03
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 4ef27c67b9b17f41fbe71d57fdea9552b7dff9f7
ms.sourcegitcommit: 2badee2b63ae63687795250e298f463474063100
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/14/2018
ms.locfileid: "45601034"
---
# <a name="monitor-cloud-management-gateway-in-configuration-manager"></a>Monitorar o gateway de gerenciamento de nuvem no Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Depois que o CMG (Gateway de Gerenciamento de Nuvem) estiver em execução e os clientes estiverem se conectando por meio dele, você poderá monitorar os clientes e o tráfego de rede para garantir que sabe como o serviço está sendo executado.



## <a name="monitor-clients"></a>Monitorar clientes

Os clientes conectados por meio do CMG são exibidos no console do Configuration Manager da mesma forma que os clientes locais. Para obter mais informações, consulte [Como monitorar clientes](/sccm/core/clients/manage/monitor-clients).



## <a name="monitor-traffic-in-the-console"></a>Monitorar o tráfego no console

Monitore o tráfego no CMG usando o console do Configuration Manager:

1. Vá para o workspace **Administração**, expanda **Serviços de Nuvem** e selecione o nó **Gateway de Gerenciamento de Nuvem**.  

2. Selecione o CMG no painel de lista.  

3. Exiba as informações de tráfego no painel de detalhes para o ponto de conexão do CMG e as funções do sistema de sites às quais ele se conecta.  



## <a name="set-up-outbound-traffic-alerts"></a>Configurar alertas de tráfego de saída

Os alertas de tráfego de saída ajudam você a saber quando o tráfego de rede se aproxima de um nível de limite de 14 dias. Quando você cria o CMG, pode configurar alertas de tráfego. Se você tiver ignorado essa parte, ainda será possível configurar os alertas depois que o serviço estiver em execução. Ajuste as configurações de alerta a qualquer momento.

1. Vá para o workspace **Administração**, expanda **Serviços de Nuvem** e selecione o nó **Gateway de Gerenciamento de Nuvem**.  

2. Selecione o CMG no painel de lista e, em seguida, selecione **Propriedades** na faixa de opções.  

3. Vá para a guia **Alertas** para habilitar o limite e alertas. Especifique o limite de dados de 14 dias em GB (gigabytes). Especifique também o percentual de limite para elevar os diferentes níveis de alerta.  

4. Quando terminar, selecione **OK**.  



## <a name="monitor-logs"></a>Monitorar os logs

O CMG gera entradas em vários arquivos de log. Para obter mais informações, consulte [Arquivos de log no System Center Configuration Manager](/sccm/core/plan-design/hierarchy/log-files#cloud-management-gateway).



## <a name="cloud-management-dashboard"></a>Painel de gerenciamento de nuvem
<!--1358461--> Começando na versão 1806, o painel de gerenciamento de nuvem fornece uma exibição centralizada para uso do CMG. Quando o site estiver integrado aos [Serviços do Azure](/sccm/core/servers/deploy/configure/azure-services-wizard) para gerenciamento de nuvem, ele também exibe dados sobre usuários e dispositivos de nuvem.  

A captura de tela a seguir é uma parte do painel de gerenciamento de nuvem que mostra dois dos blocos disponíveis:  
![O painel de controle do gerenciamento de nuvem faz o rastreamento do tráfego CMG e dos clientes online atuais](media/1358461-cmg-dashboard.png)

No console do Configuration Manager, acesse o espaço de trabalho **Monitoramento**. Selecione o nó **Gerenciamento de Nuvem** e visualize os blocos do painel.  



## <a name="connection-analyzer"></a>Analisador de conexão

Começando na versão 1806, use o analisador de conexão do CMG para verificação em tempo real para ajudar a solucionar problemas. O utilitário no console verifica o status atual do serviço e o canal de comunicação por meio da conexão CMG aponta para os pontos de gerenciamento que permitem o tráfego CMG.

1. No console do Configuration Manager, acesse o espaço de trabalho **Administração**. Expanda **Serviços de Nuvem** e selecione o nó **Gateway de Gerenciamento de Nuvem**.  

2. Selecione a instância CMG de destino e, em seguida, selecione **Analisador de Conexões** na faixa de opções.  

3. Na janela do analisador de conexões CMG, selecione uma das seguintes opções para autenticar com o serviço:  

     1. **Usuário do Azure AD**: use essa opção para simular a comunicação da mesma forma que uma identidade de usuário baseada em nuvem conectada a um dispositivo Windows 10 adicionado ao Azure AD. Clique em **Entrar** para inserir com segurança as credenciais dessa conta de usuário do Azure AD.  

     2. **Certificado de cliente**: use essa opção para simular a comunicação da mesma forma que um cliente do Configuration Manager com um [certificado de autenticação de cliente ](/sccm/core/clients/manage/cmg/certificates-for-cloud-management-gateway#client-authentication-certificate).  

4. Selecione **Iniciar** para iniciar a análise. A janela do analisador exibe os resultados. Selecione uma entrada para ver mais detalhes no campo Descrição.  

