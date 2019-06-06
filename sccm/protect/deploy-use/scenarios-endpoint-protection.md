---
title: Proteger computadores contra malware
titleSuffix: Configuration Manager
description: Aprenda a implementar o Endpoint Protection no Configuration Manager para proteger computadores contra ataques de malware.
ms.date: 05/30/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 539c7a89-3c03-4571-9cb4-02d455064eeb
author: mestew
ms.author: mstewart
manager: doubeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: e1ab204a8b04b1e19b419a6bb3ca677fab660148
ms.sourcegitcommit: 18a94eb78043cb565b05cd0e9469b939b29cccf0
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 05/29/2019
ms.locfileid: "66355088"
---
# <a name="example-scenario-use-endpoint-protection-to-protect-computers-from-malware"></a>Cenário de exemplo: usar o Endpoint Protection para proteger computadores contra malware

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Este artigo fornece um cenário de exemplo de como você pode implementar o Endpoint Protection no Configuration Manager para proteger os computadores em sua organização contra ataques de malware.  



## <a name="scenario-overview"></a>Visão geral do cenário

 O System Center Configuration Manager é instalado e usado no Woodgrove Bank. O banco atualmente usa o System Center Endpoint Protection para proteger os computadores contra ataques de malware. Além disso, o banco usa a Política de Grupo do Windows para garantir que o Firewall do Windows esteja habilitado em todos os computadores da empresa e que os usuários sejam notificados quando o Firewall do Windows bloqueia um novo programa.  

Os administradores do Configuration Manager receberam um pedido para atualizar o software antimalware do Woodgrove Bank para o System Center Endpoint Protection, para que o banco possa se beneficiar dos recursos antimalware mais recentes e possa gerenciar centralmente a solução antimalware do console do Configuration Manager. 


## <a name="business-requirements"></a>Requisitos de negócios

Essa implementação tem os seguintes requisitos:  

- Usar o Configuration Manager para gerenciar configurações do Firewall do Windows que atualmente são gerenciadas pela Política de Grupo.  

- Usar as atualizações de software do Configuration Manager para baixar as definições de malware para computadores. Se as atualizações de software não estiverem disponíveis, por exemplo, se o computador não estiver conectado à rede corporativa, os computadores deverão baixar as atualizações de definição no Microsoft Update.  

- Os computadores dos usuários devem executar uma rápida verificação de malware diariamente. Os servidores, no entanto, devem executar uma verificação completa todos os sábados, fora do horário comercial, à 01:00h.  

- Enviar um alerta por email sempre que ocorrer algum dos seguintes eventos:  

  -   Quando malware for detectado em qualquer computador  

  -   Quando a mesma ameaça de malware for detectada em mais de 5% dos computadores  

  -   A mesma ameaça de malware é detectada mais de 5 vezes em um período de 24 horas  

  -   Mais de três tipos diferentes de malware são detectados em um período de 24 horas  

  Os administradores executam as seguintes etapas para implementar o Endpoint Protection:  



##  <a name="steps-to-implement-endpoint-protection"></a>Etapas para implementar a proteção de ponto de extremidade  

|Processar|Referência|  
|-------------|---------------|  
|Os administradores analisam as informações disponíveis sobre os conceitos básicos do Endpoint Protection no Configuration Manager.|Para obter uma visão geral sobre o Endpoint Protection, consulte [Endpoint Protection no System Center Configuration Manager](endpoint-protection.md).|  
|Os administradores analisam e implementam os pré-requisitos necessários para usar o Endpoint Protection.|Para obter informações sobre os pré-requisitos do Endpoint Protection, consulte [Planejamento do Endpoint Protection](../plan-design/planning-for-endpoint-protection.md).|  
|Os administradores instalam a função de sistema de sites do Endpoint Protection em apenas um servidor de sistema de sites, no topo da hierarquia do Woodgrove Bank.|Para obter mais informações sobre como instalar a função de sistema de sites do Endpoint Protection, veja os "Pré-requisitos" em [Configurar o Endpoint Protection](configure-endpoint-protection.md).|  
|Os administradores configuram o Configuration Manager para usar um servidor SMTP para enviar alertas de email.<br /><br /> **Observação:** você precisará configurar um servidor SMTP somente se quiser ser notificado por email quando um alerta do Endpoint Protection for gerado.|Para obter mais informações, consulte [Configurar alertas no Endpoint Protection](endpoint-configure-alerts.md).|  
|Os administradores criam uma coleção de dispositivos que contém todos os computadores e servidores para instalar o cliente do Endpoint Protection. Eles chamam a coleção de **Todos os computadores protegidos pelo Endpoint Protection**.<br /><br /> **Dica:** você não pode configurar alertas para coleções de usuários.|Para obter mais informações sobre como criar coleções, consulte [Como criar coleções no System Center Configuration Manager](../../core/clients/manage/collections/create-collections.md)|  
|Os administradores configuram os seguintes alertas para a coleção: <br /><br />1) **Malware detectado**: os administradores configuram a severidade do alerta como **Crítico**. <br /><br />2) **O mesmo tipo de malware é detectado em vários computadores**: Os administradores configuram a severidade de alerta **Crítico** e especifica que o alerta será gerado quando mais de 5% dos computadores tiverem um malware detectado. <br /><br />3) **O mesmo tipo de malware é detectado repetidamente dentro do intervalo especificado em um computador**: os administradores configuram a severidade de alerta Crítico e especificam que o alerta será gerado quando um malware for detectado mais de 5 vezes em um período de 24 horas. <br /><br />4) **Vários tipos de malware são detectados no mesmo computador dentro do intervalo especificado**: os administradores configuram a severidade de alerta Crítico e especificam que o alerta será gerado quando mais de 3 tipos de malware forem gerados em um período de 24 horas.<br /><br /> O valor da **Severidade do Alerta** indica o nível de alerta que será exibido no console do Configuration Manager e nos alertas que eles recebem em uma mensagem de email.<br /><br /> Eles também selecionam a opção **Exibir esta coleção no painel do Endpoint Protection** para que possam monitorar os alertas no console do Configuration Manager.|Veja a seção “Configurar alertas para o Endpoint Protection” em [Configurando o Endpoint Protection no System Center Configuration Manager](endpoint-configure-alerts.md).|  
|Os administradores configuram as atualizações de software do Configuration Manager para baixar e implantar atualizações de definição três vezes por dia usando uma regra de implantação automática.|Para obter mais informações, veja a seção "Usando as atualizações de Software do Configuration Manager para fornecer atualizações de definições" em [Usar atualizações de software do Configuration Manager para fornecer atualizações de definições](endpoint-definitions-configmgr.md).|  
|Os administradores examinam as configurações na política de antimalware padrão, que contém as configurações de segurança da Microsoft. Para os computadores executarem uma verificação rápida diária, eles alteram as configurações a seguir:<br /><br /> 1) **Executar uma verificação rápida diária nos computadores cliente**: **Sim**.<br /><br /> 2) **Hora de agendamento da verificação rápida diária**:  **9:00 AM**.<br /><br /> Os administradores observam que as **atualizações distribuídas do Microsoft Update** são selecionadas por padrão como uma fonte de atualização de definição. Isso atende ao requisito de negócios de que os computadores baixem definições do Microsoft Update quando não puderem receber atualizações de software do Configuration Manager.|Consulte [Como criar e implantar políticas antimalware para o Endpoint Protection no System Center Configuration Manager](endpoint-antimalware-policies.md).|  
|Os administradores criam uma coleção que contém apenas os servidores do Woodgrove Bank chamada **Servidores do Woodgrove Bank**.|Consulte [Como criar coleções no System Center Configuration Manager](../../core/clients/manage/collections/create-collections.md)|  
|Os administradores criam uma política antimalware personalizada chamada **política de servidor do Woodgrove Bank**. Eles adicionam somente as configurações das **verificações agendadas** e fazem as seguintes alterações:<br /><br /> **Tipo de varredura**:  **completa**<br /><br /> **Dia da varredura**:  **sábado**<br /><br /> **Horário da varredura**: **1:00**<br /><br /> **Executar uma verificação rápida diária nos computadores cliente**:  **Não**.|Consulte [Como criar e implantar políticas antimalware para o Endpoint Protection no System Center Configuration Manager](endpoint-antimalware-policies.md).|  
|Os administradores implantam a política personalizada antimalware chamada **Política de Servidor do Woodgrove Bank** na coleção **Servidores do Woodgrove Bank**.|Consulte "Para implantar uma política antimalware em computadores cliente" no artigo [Como criar e implantar políticas antimalware para o Endpoint Protection](endpoint-antimalware-policies.md).|  
|Os administradores criam um novo conjunto de configurações personalizadas de dispositivo do cliente para o Endpoint Protection e o denominam **Configurações do Endpoint Protection do Woodgrove Bank**.<br /><br /> **Observação:** se você não quiser instalar e habilitar o Endpoint Protection em todos os clientes de sua hierarquia, verifique se as opções **Gerenciar cliente do Endpoint Protection nos computadores cliente** e **Instalar o cliente do Endpoint Protection nos computadores cliente** foram definidas como **Não** nas configurações padrão do cliente.|Para obter mais informações, consulte [Definir configurações personalizadas do cliente para o Endpoint Protection](endpoint-protection-configure-client.md).|  
|Eles definem as seguintes configurações para o Endpoint Protection:<br /><br /> **Gerenciar cliente do Endpoint Protection nos computadores cliente**:  **Sim**<br /><br /> A configuração e o valor garantem que qualquer cliente existente do Endpoint Protection que for instalado será gerenciado por Configuration Manager.<br /><br /> **Instalar o cliente do Endpoint Protection em computadores cliente**:  **Sim**.</br></br>**Observação** no Configuration Manager 1802, os dispositivos Windows 10 não precisam ter o agente do Endpoint Protection instalado. Se ele já estiver instalado nos dispositivos Windows 10, o Configuration Manager não o removerá. Os administradores podem remover o agente do Endpoint Protection dos dispositivos Windows 10 que executam, no mínimo, a versão de cliente 1802.|Para obter mais informações, consulte [Definir configurações personalizadas do cliente para o Endpoint Protection](endpoint-protection-configure-client.md).|  
|Os administradores implantam as **Configurações do Endpoint Protection do Woodgrove Bank** do cliente na coleção **Todos os computadores protegidos pelo Endpoint Protection**.|Consulte “Definir configurações personalizadas do cliente para o Endpoint Protection” em [Configurando o Endpoint Protection no Configuration Manager](endpoint-antimalware-policies.md).|  
|Os administradores usam o assistente para Criar Política de Firewall do Windows para criar uma política, definindo as seguintes configurações para o perfil de domínio:<br /><br /> 1) **Habilitar o Firewall do Windows**: **Sim**<br /><br /> 2)<br />                    **Notificar o usuário quando o Firewall do Windows bloquear um novo programa**: **Sim**|Consulte [Como criar e implantar políticas do Firewall do Windows para o Endpoint Protection no System Center Configuration Manager](../../protect/deploy-use/create-windows-firewall-policies.md)|  
|Os administradores implantam a nova política de firewall na coleção **Todos os computadores protegidos pelo Endpoint Protection** que criaram anteriormente.|Consulte "Para implantar uma política de Firewall do Windows" em [Como criar e implantar políticas do Firewall do Windows para o Endpoint Protection no System Center Configuration Manager](create-windows-firewall-policies.md)|  
|Os administradores usam as tarefas de gerenciamento disponíveis para o Endpoint Protection para gerenciar políticas antimalware e do Firewall do Windows, executar varreduras sob demanda dos computadores quando necessário, forçar os computadores a baixarem as definições mais recentes e especificar uma ação adicional a ser tomada quando malware for detectado.|Consulte [Como gerenciar políticas antimalware e configurações de firewall para o Endpoint Protection no System Center Configuration Manager](endpoint-antimalware-firewall.md)|  
|Os administradores usam os seguintes métodos para monitorar o status do Endpoint Protection e as ações tomadas pelo Endpoint Protection:<br /><br /> 1) Usando o nó **Status do Endpoint Protection** em **Segurança** no workspace **Monitoramento**.<br /><br /> 2) Usar o nó o **Endpoint Protection** no workspace **Ativos e Conformidade**.<br /><br /> 3) Usar os relatórios internos do Configuration Manager.|Consulte [Como monitorar o Endpoint Protection no System Center Configuration Manager](monitor-endpoint-protection.md)|  

 Os administradores relatam uma implementação bem-sucedida do Endpoint Protection ao gerente deles e confirmam que os computadores do Woodgrove Bank estão protegidos contra malware, de acordo com os requisitos de negócios que eles receberam. 

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações, consulte [Como configurar o Endpoint Protection](/sccm/protect/deploy-use/endpoint-protection-configure)