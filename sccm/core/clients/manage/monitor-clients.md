---
title: "Monitorar clientes – Configuration Manager | Microsoft Docs"
description: "Obtenha orientações detalhadas sobre como monitorar clientes no System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-client
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2c8f57cf-1968-48de-87fb-4897432ed6e0
caps.latest.revision: 23
author: arob98
ms.author: angrobe
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 3743c80b0c2b5142f3a537ba3855ffd14794d42b
ms.openlocfilehash: 85afe010e734d20ae1f1479b3edd166c54cc8fd2
ms.lasthandoff: 01/24/2017


---
# <a name="how-to-monitor-clients-in-system-center-configuration-manager"></a>Como monitorar clientes no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*


 Depois que o aplicativo cliente do System Center Configuration Manager tiver sido instalado nos computadores e dispositivos com Windows no seu site, você poderá monitorar a integridade e a atividade deles no console do Configuration Manager.  

##  <a name="a-namebkmkabouta-about-client-status"></a><a name="bkmk_about"></a> Sobre o status do cliente  
 O Configuration Manager fornece os seguintes tipos de informação como status do cliente:  

-   **Status online do cliente** ‑ A partir da versão 1602 do Configuration Manager, esse status indica se o computador está online ou não. Um computador será considerado online se estiver conectado ao seu ponto de gerenciamento atribuído.  Para indicar se o cliente está online, ele envia mensagens como ping ao ponto de gerenciamento. Se o ponto de gerenciamento não receber uma mensagem no tempo médio de cinco minutos, o cliente será considerado offline.  

-   **Atividade do cliente** ‑ Esse status indica se o cliente esteve ativamente envolvido com o Configuration Manager nos últimos 7 dias. Se o cliente não tiver solicitado uma atualização de política, enviado uma mensagem de pulsação ou enviado um inventário de hardware nos 7 dias, ele será considerado inativo.  

-   **Verificação do cliente** ‑ esse status indica o êxito da avaliação periódica que o cliente do Configuration Manager executa no computador.  A avaliação verifica o computador e pode corrigir alguns dos problemas encontrados. Para saber mais, veja [Verificações e correções feitas pela verificação do cliente](#BKMK_ClientHealth).  

     Em computadores que executam o Windows 7, a verificação do cliente é executada como uma tarefa agendada. Em sistemas operacionais posteriores, a verificação do cliente é executada automaticamente durante a janela de manutenção do Windows.  

     Você pode configurar a correção para não ser executada em computadores específicos, por exemplo, um servidor importante para os negócios. Além disso, se houver itens adicionais que você deseja avaliar, você poderá usar as configurações de conformidade do Configuration Manager para fornecer uma solução abrangente para monitorar a integridade geral, a atividade e a conformidade de computadores na organização. Para obter mais informações sobre as configurações de conformidade, veja [Planejando e configurando as configurações de conformidade no System Center Configuration Manager](../../../compliance/plan-design/plan-for-and-configure-compliance-settings.md).  

##  <a name="a-namebkmkindstatusa-monitor-the-status-of-individual-clients"></a><a name="bkmk_indStatus"></a> Monitorar o status de clientes individuais  

1.  No console do Configuration Manager, clique em **Ativos e Conformidade** > **Dispositivos** ou escolha uma coleção em **Coleções de Dispositivos**.  

     A partir da versão 1602 do Configuration Manager, os ícones no início de cada linha indicam o status online do dispositivo:  

    |||  
    |-|-|  
    |![ícone de status online para clientes](../../../core/clients/manage/media/online-status-icon.png)|O dispositivo está online.|  
    |![ícone de status offline para clientes](../../../core/clients/manage/media/offline-status-icon.png)|O dispositivo está offline.|  
    |![ícone de status desconhecido para clientes](../../../core/clients/manage/media/unknown-status-icon.png)|O status online é desconhecido.|  
    |![cliente não instalado](../../../core/clients/manage/media/client-not-installed.png)|O cliente não está instalado no dispositivo.|  

2.  Para obter o status online mais detalhado, adicione as informações do status online do cliente à exibição do dispositivo clicando com o botão direito do mouse no cabeçalho da coluna e clicando nos campos de status online que deseja adicionar. As colunas que você pode adicionar são  

    -   **Status Online do Dispositivo** indica se o cliente ainda está online ou offline no momento. (É a mesma informação fornecida pelos ícones).  

    -   **Última Vez Online** indica quando o status do cliente mudou para online.  

    -   **Última Vez Offline** indica quando o status mudou para offline.  

3.  Clique em um cliente individual no painel de lista para ver mais status no painel de detalhes, incluindo informações sobre a atividade e as verificações do cliente.  

##  <a name="a-namebkmkallstatusa-monitor-the-status-of-all-clients"></a><a name="bkmk_allStatus"></a> Monitorar o status de todos os clientes  

1.  No console do Configuration Manager, clique em **Monitoramento** > **Status do Cliente**. Nessa página do console, você pode examinar as estatísticas gerais da atividade e das verificações do cliente em todo o site.  Também é possível alterar o escopo das informações ao escolher outra coleção.  

2.  Para fazer drill down nos detalhes sobre as estatísticas relatadas, clique no nome das informações relatadas (como **Clientes ativos que passaram na verificação do cliente ou sem resultados**) e examine as informações sobre os clientes individuais.  

3.  Clique em **Atividade do Cliente** para ver gráficos ilustrando a atividade do cliente em seu site do Configuration Manager.  

4.  Clique em **Verificação do Cliente** para ver gráficos ilustrando as verificações do cliente em seu site do Configuration Manager.  

 Você pode configurar alertas para notificar quando os clientes verificam resultados ou a atividade do cliente fica abaixo de uma porcentagem especificada de cliente em uma coleção ou quando a correção fica em uma porcentagem especificada de cliente. Para obter informações sobre como configurar o status do cliente, consulte [Como configurar o status do cliente no System Center Configuration Manager](../../../core/clients/deploy/configure-client-status.md).  

##  <a name="a-namebkmkclienthealtha-checks-and-remediations-made-by-client-check"></a><a name="BKMK_ClientHealth"></a> Verificações e correções feitas pela verificação do cliente  
 As seguintes verificações e correções podem ser executadas pela verificação do cliente.  

|Verificação do Cliente|Ação de correção|Mais informações|  
|------------------|------------------------|----------------------|  
|Verificar se a verificação do cliente foi executada recentemente|Executar verificação do cliente|Verifica se a verificação do cliente foi executada pelo menos uma vez nos últimos três dias.|  
|Verificar se os pré-requisitos do cliente estão instalados|Instalar os pré-requisitos do cliente|Verifica se os pré-requisitos do cliente estão instalados. Lê o arquivo ccmsetup.xml na pasta de instalação do cliente para descobrir os pré-requisitos.|  
|Teste de integridade do repositório WMI|Reinstalar o cliente do Configuration Manager|Verifica se as entradas do cliente do Configuration Manager estão presentes no WMI.|  
|Verificar se o serviço do cliente está em execução|Iniciar o serviço (Host de Agente do SMS) do cliente|Nenhuma informação adicional|  
|Teste do coletor de eventos WMI.|Reiniciar o serviço do cliente|Verifica se o Configuration Manager relacionado ao coletor de eventos WMI está perdido|  
|Verifique se existe o serviço WMI (Instrumentação de Gerenciamento do Windows)|Sem correção|Nenhuma informação adicional|  
|Verificar se o cliente foi instalado corretamente|Reinstalar o cliente|Nenhuma informação adicional|  
|Teste de leitura e gravação do repositório WMI|Redefinir o repositório WMI e reinstalar o cliente do Configuration Manager|A correção dessa verificação do cliente é realizada somente em computadores que executam o Windows Server 2003, o Windows XP (64 bits) ou versões anteriores.|  
|Verificar se o tipo de inicialização do serviço antimalware é automático|Redefinir o tipo de inicialização do serviço como automático|Nenhuma informação adicional|  
|Verificar se o serviço antimalware está em execução|Iniciar o serviço de antimalware|Nenhuma informação adicional|  
|Verificar se o tipo de inicialização do serviço Windows Update é automático ou manual|Redefinir o tipo de inicialização do serviço como automático|Nenhuma informação adicional|  
|Verificar se o tipo de inicialização de serviço (Host de Agente do SMS) do cliente é automático|Redefinir o tipo de inicialização do serviço como automático|Nenhuma informação adicional|  
|Verificar se o serviço WMI (Instrumentação de Gerenciamento do Windows) está em execução.|Iniciar o serviço de Instrumentação de Gerenciamento do Windows|Nenhuma informação adicional|  
|Verificar se o banco de dados do Microsoft SQL CE é íntegro|Reinstalar o cliente do Configuration Manager|Nenhuma informação adicional|  
|Teste de integridade do WMI da Microsoft Policy Platform|Reparar a Microsoft Policy Platform|Nenhuma informação adicional|  
|Verificar se o serviço Microsoft Policy Platform existe|Reparar a Microsoft Policy Platform|Nenhuma informação adicional|  
|Verificar se o tipo de inicialização do serviço Microsoft Policy Platform é manual|Redefinir o tipo de inicialização do serviço como manual|Nenhuma informação adicional|  
|Verificar se existe o Serviço de Transferência Inteligente de Plano de Fundo|Sem correção|Nenhuma informação adicional|  
|Verificar se o tipo de inicialização do Serviço de Transferência Inteligente de Plano de Fundo é automático ou manual|Redefinir o tipo de inicialização do serviço como automático|Nenhuma informação adicional|  
|Verificar se o tipo de inicialização do Serviço de Inspeção de Rede é manual|Redefinir o tipo de inicialização do serviço como manual se instalado|Nenhuma informação adicional|  
|Verificar se o tipo de inicialização do serviço WMI (Instrumentação de Gerenciamento do Windows) é automático|Redefinir o tipo de inicialização do serviço como automático|Nenhuma informação adicional|  
|Verificar se o tipo de inicialização de serviço do Windows Update em computadores Windows 8 é automático ou manual|Redefinir o tipo de inicialização do serviço como manual|Nenhuma informação adicional|  
|Verificar se o serviço de cliente (Host de Agente do SMS) existe.|Sem correção|Nenhuma informação adicional|  
|Verificar se o tipo de inicialização do serviço Controle Remoto do Configuration Manager é automático ou manual|Redefinir o tipo de inicialização do serviço como automático|Nenhuma informação adicional|  
|Verificar se o serviço Controle Remoto do Configuration Manager está em execução|Iniciar o serviço de controle remoto|Nenhuma informação adicional|  
|Verificar se o provedor WMI do cliente está íntegro|Reiniciar o serviço de Instrumentação de Gerenciamento do Windows|A correção dessa verificação do cliente é realizada somente em computadores que executam o Windows Server 2003, Windows XP (64 bits) ou versões anteriores.|  
|Verificar se o serviço de proxy de ativação está em execução (Proxy de ativação do ConfigMgr)|Iniciar o serviço Proxy de ativação do ConfigMgr|Esta verificação do cliente é feita apenas se a configuração **Gerenciamento de Energia**: **Habilitar proxy de ativação** estiver definida como **Sim** em sistemas operacionais do cliente com suporte.|  
|Verificar se o tipo de inicialização do serviço de proxy de ativação (Proxy de ativação do ConfigMgr) é automático|Redefinir o tipo de inicialização do serviço Proxy do ConfigMgr ativação como automático|Esta verificação do cliente é feita apenas se a configuração **Gerenciamento de Energia**: **Habilitar proxy de ativação** estiver definida como **Sim** em sistemas operacionais do cliente com suporte.|  

