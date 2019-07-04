---
title: Monitorar o gateway de gerenciamento de nuvem
titleSuffix: Configuration Manager
description: Monitore os clientes e o tráfego de rede por meio do CMG (gateway de gerenciamento de nuvem).
ms.date: 06/17/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 15f72f80-9850-40ce-9c3a-443ba04b6a03
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: d184118e0e99231a9160322740ab7690488a28a5
ms.sourcegitcommit: 3936b869d226cea41fa0090e2cbc92bd530db03a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/20/2019
ms.locfileid: "67286759"
---
# <a name="monitor-cloud-management-gateway"></a>Monitorar o gateway de gerenciamento de nuvem

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Depois que o CMG (Gateway de Gerenciamento de Nuvem) estiver em execução e os clientes estiverem se conectando por meio dele, você poderá monitorar os clientes e o tráfego de rede para garantir que sabe como o serviço está sendo executado.


## <a name="monitor-clients"></a>Monitorar clientes

Os clientes conectados por meio do CMG são exibidos no console do Configuration Manager da mesma forma que os clientes locais. Para obter mais informações, consulte [Como monitorar clientes](/sccm/core/clients/manage/monitor-clients).


## <a name="monitor-traffic-in-the-console"></a>Monitorar o tráfego no console

Monitore o tráfego no CMG usando o console do Configuration Manager:

1. Vá para o workspace **Administração**, expanda **Serviços de Nuvem** e selecione o nó **Gateway de Gerenciamento de Nuvem**.  

2. Selecione o CMG no painel de lista.  

3. Exiba as informações de tráfego no painel de detalhes para o ponto de conexão do CMG e as funções do sistema de sites às quais ele se conecta. Essas estatísticas mostram as solicitações do cliente que chegam a essas funções. As solicitações incluem a política, o local, o registro, o conteúdo, o inventário e as notificações do cliente.<!-- SCCMDocs#1208 -->

## <a name="set-up-outbound-traffic-alerts"></a>Configurar alertas de tráfego de saída

Os alertas de tráfego de saída ajudam você a saber quando o tráfego de rede se aproxima de um nível de limite de 14 dias. Quando você cria o CMG, pode configurar alertas de tráfego. Se você tiver ignorado essa parte, ainda será possível configurar os alertas depois que o serviço estiver em execução. Ajuste as configurações de alerta a qualquer momento.

1. Vá para o workspace **Administração**, expanda **Serviços de Nuvem** e selecione o nó **Gateway de Gerenciamento de Nuvem**.  

2. Selecione o CMG no painel de lista e, em seguida, selecione **Propriedades** na faixa de opções.  

3. Vá para a guia **Alertas** para habilitar o limite e alertas. Especifique o limite de dados de 14 dias em GB (gigabytes). Especifique também o percentual de limite para elevar os diferentes níveis de alerta.  

4. Quando terminar, selecione **OK**.  


## <a name="monitor-logs"></a>Monitorar os logs

O CMG gera entradas em vários arquivos de log. Para obter mais informações, consulte [Arquivos de log no System Center Configuration Manager](/sccm/core/plan-design/hierarchy/log-files#cloud-management-gateway).


## <a name="cloud-management-dashboard"></a>Painel de gerenciamento de nuvem

<!--1358461-->
Começando na versão 1806, o painel de gerenciamento de nuvem fornece uma exibição centralizada para uso do CMG. Quando o site estiver integrado aos [Serviços do Azure](/sccm/core/servers/deploy/configure/azure-services-wizard) para gerenciamento de nuvem, ele também exibe dados sobre usuários e dispositivos de nuvem.  

A captura de tela a seguir é uma parte do painel de gerenciamento de nuvem que mostra dois dos blocos disponíveis:  
![O painel de controle do gerenciamento de nuvem faz o rastreamento do tráfego CMG e dos clientes online atuais](media/1358461-cmg-dashboard.png)

No console do Configuration Manager, acesse o workspace **Monitoramento**. Selecione o nó **Gerenciamento de Nuvem** e visualize os blocos do painel.  


## <a name="connection-analyzer"></a>Analisador de conexão

Começando na versão 1806, use o analisador de conexão do CMG para verificação em tempo real para ajudar a solucionar problemas. O utilitário no console verifica o status atual do serviço e o canal de comunicação por meio da conexão CMG aponta para os pontos de gerenciamento que permitem o tráfego CMG.

1. No console do Configuration Manager, acesse o workspace **Administração**. Expanda **Serviços de Nuvem** e selecione o nó **Gateway de Gerenciamento de Nuvem**.  

2. Selecione a instância CMG de destino e, em seguida, selecione **Analisador de Conexões** na faixa de opções.  

3. Na janela do analisador de conexões CMG, selecione uma das seguintes opções para autenticar com o serviço:  

     1. **Usuário do Azure AD**: use essa opção para simular a comunicação da mesma forma que uma identidade de usuário baseada em nuvem conectada a um dispositivo Windows 10 adicionado ao Azure AD. Clique em **Entrar** para inserir com segurança as credenciais dessa conta de usuário do Azure AD.  

     2. **Certificado de cliente**: use essa opção para simular a comunicação da mesma forma que um cliente do Configuration Manager com um [certificado de autenticação de cliente ](/sccm/core/clients/manage/cmg/certificates-for-cloud-management-gateway#bkmk_clientauth).  

4. Selecione **Iniciar** para iniciar a análise. A janela do analisador exibe os resultados. Selecione uma entrada para ver mais detalhes no campo Descrição.  


## <a name="bkmk_stop"></a> Interromper o CMG quando ele exceder o limite

<!--3735092-->
A partir da versão 1902, o Configuration Manager pode parar um serviço CMG quando a transferência de dados total ultrapassar o limite. Use [alertas](#set-up-outbound-traffic-alerts) para disparar notificações quando o uso atingir níveis de aviso ou críticos. Para ajudar a reduzir os custos inesperados do Azure devido a um aumento do uso, esta opção desabilita o serviço de nuvem.

> [!Important]  
> Mesmo se o serviço não estiver em execução, ainda haverá custos associados ao serviço de nuvem. A interrupção do serviço não elimina todos os custos do Azure associados. Para remover todos os custos do serviço de nuvem [remova o CMG](/sccm/core/clients/manage/cmg/setup-cloud-management-gateway#modify-a-cmg).  
>
> Quando o serviço CMG é interrompido, os clientes baseados na Internet não podem se comunicar com o Configuration Manager.  

A transferência de dados total (saída) inclui dados da conta de armazenamento e do serviço de nuvem. Esses dados são provenientes dos seguintes fluxos:

- CMG para o cliente  
- CMG para o site, inclusive arquivos de log do CMG  
- Se você habilitar o CMG para conteúdo, conta de armazenamento para o cliente  

Para obter mais informações sobre esses fluxos de dados, confira [Portas e fluxo de dados do CMG](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway#ports-and-data-flow).

O limite de alerta de armazenamento é separado. Esse alerta monitora a capacidade da sua instância de Armazenamento do Azure.

Ao selecionar a instância do CMG no nó **Gateway de Gerenciamento de Nuvem** no console, você pode ver o total de transferência de dados no painel de detalhes.

O Configuration Manager verifica o valor limite a cada seis minutos. Se houver um aumento repentino no uso, o Configuration Manager poderá levar até seis minutos para detectar que excedeu o limite e interromper o serviço.

### <a name="process-to-stop-the-cloud-service-when-it-exceeds-threshold"></a>Continue até interromper o serviço de nuvem quando ele exceder o limite

1. [Configurar alertas de tráfego de saída](#set-up-outbound-traffic-alerts).  

2. Na guia **Alertas** da janela de propriedades do CMG, habilite a opção para **Interromper esse serviço quando o limite crítico for excedido**.  

Para testar esse recurso, reduza temporariamente um dos seguintes valores:  

- **Limite de 14 dias para transferência de dados de saída (GB)** . O valor padrão é `10000`.  

- **Percentual de limite para emitir um alerta Crítico:** . O valor padrão é `90`.  
