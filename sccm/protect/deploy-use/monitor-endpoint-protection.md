---
title: Monitorar o status do Endpoint Protection | Microsoft Docs
description: Saiba como monitorar o Endpoint Protection na sua hierarquia do System Center Configuration Manager.
ms.custom: na
ms.date: 12/9/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f4a1335c-bb3d-493e-a124-83a32a107dc8
caps.latest.revision: 8
author: NathBarn
ms.author: nathbarn
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 0fa837c68eb073d2ceaf48c938137a94141a102e
ms.openlocfilehash: 99e266e44f718d97c2a6e61e8e6816752751ed7b


---
# <a name="how-to-monitor-endpoint-protection-status"></a>Como monitorar o status do Endpoint Protection

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Você pode monitorar o Endpoint Protection na sua hierarquia do Microsoft System Center Configuration Manager usando o nó **Status do Endpoint Protection** em **Segurança** no espaço de trabalho **Monitoramento**, no nó **Endpoint Protection** no espaço de trabalho **Ativos e Conformidade** e usando relatórios.  

##  <a name="a-namebkmk1a-how-to-monitor-endpoint-protection-by-using-the-endpoint-protection-status-node"></a><a name="BKMK_1"></a> Como monitorar o Endpoint Protection usando o Nó de Status do Endpoint Protection  

1.  No console do Configuration Manager, clique em **Monitoramento**.  

2.  No espaço de trabalho **Monitoramento**, expanda **Segurança** e clique em **Status do Endpoint Protection**.  

3.  No **coleção** lista, selecione a coleção para a qual você deseja exibir informações de status.  

    > [!IMPORTANT]  
    >  Coleções estão disponíveis para seleção nos seguintes casos:  
    >   
    >  -   Quando você seleciona **Exibir esta coleção no painel do Endpoint Protection** na guia **Alertas** da caixa de diálogo *Propriedades\>***<nome da coleção**.  
    > -   Quando você implanta uma política antimalware do Endpoint Protection à coleção.  
    > -   Quando você habilita e implanta as configurações do cliente do Endpoint Protection na coleção.  

4.  Revise as informações exibidas de **o estado de segurança** e **estado operacional** seções. Você pode clicar em qualquer link de status para criar uma coleção temporária no **dispositivos** nó o **ativos e conformidade** espaço de trabalho. A coleção temporária contém os computadores com o status selecionado.  

    > [!IMPORTANT]  
    >  As informações exibidas no nó **Status do Endpoint Protection** baseia-se nos dados últimos que foram resumidos do banco de dados do Configuration Manager e podem não ser atuais. Se você deseja recuperar os dados mais recentes, na guia **Início** clique em **Executar Resumo**, ou clique em **Agendar Resumo** para ajustar o intervalo de resumo.  

##  <a name="a-namebkmk2a-how-to-monitor-endpoint-protection-in-the-assets-and-compliance-workspace"></a><a name="BKMK_2"></a> Como monitorar o Endpoint Protection no espaço de trabalho Ativos e Conformidade  

1.  No console do Configuration Manager, clique em **Ativos e Conformidade**.  

2.  No **ativos e conformidade** espaço de trabalho, execute uma das seguintes ações:  

    -   Clique em **dispositivos**. No **dispositivos** lista, selecione um computador e, em seguida, clique no **detalhes de Malware** guia.  

    -   Clique em **coleções de dispositivos**. Na lista **Coleções de Dispositivos** , selecione a coleção que contém o computador que você deseja monitorar e, na guia **Início** , no grupo **Coleção** , clique em **Mostrar Membros**.  

3.  Na lista *<nome da coleção\>*, selecione um computador e clique na guia **Detalhe do Malware**.  

##  <a name="a-namebkmk3a-how-to-monitor-endpoint-protection-by-using-reports"></a><a name="BKMK_3"></a> Como monitorar o Endpoint Protection usando relatórios  
 Use os relatórios a seguir para ajudar a exibir informações sobre o Endpoint Protection na sua hierarquia. Você também pode usar esses relatórios para ajudar a solucionar quaisquer problemas com o Endpoint Protection. Para obter mais informações sobre como configurar relatórios no Configuration Manager, consulte [Relatórios no System Center Configuration Manager](../../core/servers/manage/reporting.md) e [Arquivos de log no System Center Configuration Manager](../../core/plan-design/hierarchy/log-files.md). Os relatórios do Endpoint Protection encontram-se na pasta do Endpoint Protection.  

|Nome do relatório|Descrição|  
|-----------------|-----------------|  
|**Relatório de atividade de antimalware**|Exibe uma visão geral das atividades de antimalware para uma coleção especificada.|  
|**Computadores infectados**|Exibe uma lista de computadores em que for detectada uma ameaça especificada.|  
|**Principais usuários ameaças**|Exibe uma lista de usuários com o maior número de ameaças detectadas.|  
|**Lista de ameaças do usuário**|Exibe uma lista de ameaças que foi localizado para a conta de usuário especificada.|  

## <a name="malware-alert-levels"></a>Níveis de alerta de malware  
 Use a tabela a seguir para identificar os diferentes níveis de alerta do Endpoint Protection que podem ser exibidos em relatórios ou no console do Configuration Manager.  

|Nível de alerta|Descrição|  
|-----------------|-----------------|  
|**Falha**|Falha no Endpoint Protection ao corrigir o malware. Verifique os logs para obter detalhes do erro.<br /><br /> **Observação:** para obter uma lista de arquivos de log do Configuration Manager e Endpoint Protection, consulte a seção “Endpoint Protection” no tópico [Arquivos de Log no System Center Configuration Manager](../../core/plan-design/hierarchy/log-files.md).|  
|**Removido**|O Endpoint Protection removeu o malware com êxito.|  
|**Em Quarentena**|O Endpoint Protection moveu o malware para um local seguro e impediu sua execução até você removê-lo ou permitir que ele seja executado.|  
|**Limpo**|O malware foi limpo do arquivo infectado.|  
|**Permitido**|Um usuário administrativo selecionado para permitir que o software que contém o malware seja executado.|  
|**Nenhuma ação**|O Endpoint Protection não realizou nenhuma ação no malware. Isso pode ocorrer se o computador for reiniciado depois que o malware é detectado e o malware não for detectado; Por exemplo, se a unidade de rede mapeada no qual malware detectado não é reconectado quando o computador for reiniciado.|  
|**Bloqueado**|O Endpoint Protection bloqueou a execução do malware. Isso pode ocorrer se houver um processo no computador para conter malware.|



<!--HONumber=Jan17_HO4-->


