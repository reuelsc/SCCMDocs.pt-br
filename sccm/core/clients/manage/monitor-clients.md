---
title: Monitorar clientes
titleSuffix: Configuration Manager
description: Obter orientações detalhadas sobre como monitorar clientes no Configuration Manager
ms.date: 05/31/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 2c8f57cf-1968-48de-87fb-4897432ed6e0
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 55fd698ac5213a3b11b207d0625d953f687e319f
ms.sourcegitcommit: 65753c51fbf596f233fc75a5462ea4a44005c70b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/03/2019
ms.locfileid: "66463038"
---
# <a name="how-to-monitor-clients-in-configuration-manager"></a>Como monitorar clientes no Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Depois de instalar o cliente do Configuration Manager nos dispositivos Windows no seu site, monitore a integridade e a atividade no console do Configuration Manager.  


## <a name="bkmk_about"></a> Sobre o status do cliente

O Configuration Manager fornece os seguintes tipos de informação como status do cliente:  

- **Status online do cliente**: o site considera um dispositivo como **online** se ele estiver conectado ao seu ponto de gerenciamento atribuído. Para indicar se o cliente está online, ele envia mensagens como ping ao ponto de gerenciamento. Se o ponto de gerenciamento não receber uma mensagem em cinco minutos, o site considera o cliente como **offline**.  

- **Atividade do cliente**: o site considera o cliente como **ativo** se ele tiver comunicado com o Configuration Manager nos últimos sete dias. O site considera o cliente como **inativo** se ele ainda não solicitou feito nas seguintes ações em sete dias:  

    - Solicitou a atualização da política  
    - Enviou uma mensagem de pulsação  
    - Enviou o inventário de hardware  

- **Verificação do cliente**: o estado da avaliação periódica que o cliente do Configuration Manager executa no dispositivo. A avaliação verifica o dispositivo e pode corrigir alguns dos problemas encontrados. Para obter mais informações, confira [Verificações de integridade do cliente](#BKMK_ClientHealth).  

     Em dispositivos que executam o Windows 7, a verificação do cliente é executada como uma tarefa agendada. Em versões de sistemas operacionais posteriores, a verificação do cliente é executada automaticamente durante a janela de manutenção do Windows.  

     Você pode configurar a correção para não ser executada em dispositivos específicos, por exemplo, um servidor importante para os negócios. Se houver itens adicionais que você deseja avaliar, use as configurações de conformidade do Configuration Manager para monitorar as configurações adicionais. Para obter mais informações sobre as configurações de conformidade, veja [Planejando e configurando as configurações de conformidade](/sccm/compliance/plan-design/plan-for-and-configure-compliance-settings).  

- **Encerrado**: o site marcou o registro de dispositivo para exclusão. Esse comportamento pode ocorrer quando um novo registro para o mesmo dispositivo atribui um site primário igual ou diferente em uma hierarquia. O site exclui esses dispositivos na próxima vez que executar a tarefa de manutenção do site **Excluir dados antigos de descoberta**.<!-- SCCMDocs issue #1418 -->  

- **Obsoleto**: o site descobriu um novo registro de dispositivo com a mesma ID de hardware, portanto, ele marca o registro antigo como obsoleto. Os relatórios não contam registros obsoletos do mesmo dispositivo várias vezes. Você ainda pode direcionar políticas para dispositivos obsoletos. Se o site não receber uma pulsação para um registro obsoleto após 90 dias de inatividade, ele remove o dispositivo obsoleto ao executar a tarefa de manutenção do site **Excluir dados de descoberta de cliente obsoleto**.


## <a name="bkmk_indStatus"></a> Monitorar clientes individuais

1. No console do Configuration Manager, vá até o workspace **Ativos e conformidade**. Selecione o nó **Dispositivos** ou escolha uma coleção em **Coleções de dispositivos**.  

    Os ícones no início de cada linha indicam o status online do dispositivo:  

    |||  
    |-|-|  
    |![ícone de status online para clientes](../../../core/clients/manage/media/online-status-icon.png)|O dispositivo está online|  
    |![ícone de status offline para clientes](../../../core/clients/manage/media/offline-status-icon.png)|O dispositivo está offline|  
    |![ícone de status desconhecido para clientes](../../../core/clients/manage/media/unknown-status-icon.png)|O status online é desconhecido|  
    |![cliente não instalado](../../../core/clients/manage/media/client-not-installed.png)|Cliente não está instalado no dispositivo|  

2. Para obter um status online mais detalhado, adicione as informações de status online do cliente à exibição do dispositivo. Clique com botão direito do mouse no cabeçalho da coluna e selecione os campos de status online que você deseja adicionar:

    - **Status online do dispositivo**: indica se o cliente ainda está online ou offline no momento. (Este status é a mesma informação fornecida pelos ícones.)  

    - **Última vez online**: indica quando o status do cliente mudou para online  

    - **Última vez offline**: indica quando o status mudou para offline  

3. Selecione um cliente individual no painel de lista para ver mais status no painel de detalhes. Essas informações incluem a atividade do cliente e o status de verificação do cliente.  


## <a name="bkmk_allStatus"></a> Monitorar o status de todos os clientes

1. No console do Configuration Manager, acesse o workspace **Monitoramento** e selecione o nó **Status do Cliente**. Examine as estatísticas gerais da atividade do cliente e as verificações do cliente no site. Altere o escopo das informações ao escolher outra coleção.  

2. Para fazer drill down nos detalhes sobre as estatísticas relatadas, escolha o nome das informações relatadas. Por exemplo, **Clientes ativos que passaram na verificação do cliente ou não tiveram resultado**. Em seguida, examine as informações sobre os clientes individuais.  

3. Selecione **Atividade do Cliente** para ver gráficos exibindo a atividade do cliente em seu site do Configuration Manager.  

4. Selecione **Verificação do Cliente** para ver gráficos, exibindo as verificações do cliente em seu site do Configuration Manager.  

    Configure alertas para notificá-lo quando os resultados da verificação do cliente ou a atividade do cliente cai abaixo de um percentual especificado. O site também pode alertar você quando a correção falha em um percentual especificado de clientes. Para obter mais informações, consulte [Como configurar o status do cliente](/sccm/core/clients/deploy/configure-client-status).  


## <a name="BKMK_ClientHealth"></a> Verificações de integridade do cliente

A verificação do cliente executa as seguintes verificações e correções:  

|Verificação do Cliente|Ação de correção|Mais informações|  
|------------------|------------------------|----------------------|  
|Verificar se a verificação do cliente foi executada recentemente|Executar verificação do cliente|Verifica se a verificação do cliente foi executada pelo menos uma vez nos últimos três dias.|  
|Verificar se os pré-requisitos do cliente estão instalados|Instalar os pré-requisitos do cliente|Verifica se os pré-requisitos do cliente estão instalados. Lê o arquivo ccmsetup.xml na pasta de instalação do cliente para descobrir os pré-requisitos.|  
|Teste de integridade do repositório WMI|Reinstalar o cliente do Configuration Manager|Verifica se as entradas do cliente do Configuration Manager estão presentes no WMI.|  
|Verificar se o serviço do cliente está em execução|Iniciar o serviço (Host de Agente do SMS) do cliente|Nenhuma informação adicional|  
|Teste do coletor de eventos WMI.|Reiniciar o serviço do cliente|Verifica se o Configuration Manager relacionado ao coletor de eventos WMI está perdido|  
|Verifique se existe o serviço WMI (Instrumentação de Gerenciamento do Windows)|Sem correção|Nenhuma informação adicional|  
|Verificar se o cliente foi instalado corretamente|Reinstalar o cliente|Nenhuma informação adicional|  
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
|Verificar se o tipo de inicialização de serviço do Windows Update em dispositivos Windows 8 é automático ou manual|Redefinir o tipo de inicialização do serviço como manual|Nenhuma informação adicional|  
|Verificar se o serviço de cliente (Host de Agente do SMS) existe.|Sem correção|Nenhuma informação adicional|  
|Verificar se o tipo de inicialização do serviço Controle Remoto do Configuration Manager é automático ou manual|Redefinir o tipo de inicialização do serviço como automático|Nenhuma informação adicional|  
|Verificar se o serviço Controle Remoto do Configuration Manager está em execução|Iniciar o serviço de controle remoto|Nenhuma informação adicional|  
|Verificar se o serviço de proxy de ativação está em execução (Proxy de ativação do ConfigMgr)|Iniciar o serviço Proxy de ativação do ConfigMgr|Essa verificação de cliente só será feita se a configuração do cliente **Gerenciamento de Energia**: **Habilitar proxy de ativação** estiver definida como **Sim** em sistemas operacionais do cliente com suporte.|  
|Verificar se o tipo de inicialização do serviço de proxy de ativação (Proxy de ativação do ConfigMgr) é automático|Redefinir o tipo de inicialização do serviço Proxy do ConfigMgr ativação como automático|Essa verificação de cliente só será feita se a configuração do cliente **Gerenciamento de Energia**: **Habilitar proxy de ativação** estiver definida como **Sim** em sistemas operacionais do cliente com suporte.|  


<!-- 
5/31/2019 ACz: need to confirm if these checks are still applicable
|WMI repository read and write test|Reset the WMI repository and reinstall the Configuration Manager client|Remediation of this client check is only performed on devices that run Windows Server 2003, Windows XP (64-bit) or earlier versions.|  
|Verify that the client WMI provider is healthy|Restart the Windows Management Instrumentation service|Remediation of this client check is only performed on devices that run Windows Server 2003, Windows XP (64-bit) or earlier.|  
 -->


## <a name="client-deployment-log-files"></a>Arquivos de log de implantação de cliente

Para obter mais informações sobre os arquivos de log usado por operações de gerenciamento e implantação do cliente, confira [Arquivos de log](/sccm/core/plan-design/hierarchy/log-files#BKMK_ClientLogs).
