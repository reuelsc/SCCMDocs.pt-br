---
title: Proteger computadores contra malware
titleSuffix: Configuration Manager
description: Aprenda a implementar o Endpoint Protection no Configuration Manager para proteger computadores contra ataques de malware.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 539c7a89-3c03-4571-9cb4-02d455064eeb
author: aczechowski
ms.author: aaroncz
manager: doubeby
ms.openlocfilehash: 0f10194b712964b419d8951a5ba496458cb15f3b
ms.sourcegitcommit: 48098f9fb2f447672bf36d50c9f58a3d26acb9ed
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2018
ms.locfileid: "53422990"
---
# <a name="example-scenario-use-endpoint-protection-to-protect-computers-from-malware"></a>Cenário de exemplo: usar o Endpoint Protection para proteger computadores contra malware

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Este artigo fornece um cenário de exemplo de como você pode implementar o Endpoint Protection no Configuration Manager para proteger os computadores em sua organização contra ataques de malware.  



## <a name="scenario-overview"></a>Visão geral do cenário

João é o administrador do Configuration Manager no Banco Woodgrove. O banco atualmente usa o System Center Endpoint Protection para proteger os computadores contra ataques de malware. Além disso, o banco usa a Política de Grupo do Windows para garantir que o Firewall do Windows esteja habilitado em todos os computadores da empresa e que os usuários sejam notificados quando o Firewall do Windows bloqueia um novo programa.  

João recebeu um pedido para atualizar o software antimalware do Banco Woodgrove para o System Center Endpoint Protection, para que o banco possa se beneficiar dos recursos antimalware mais recentes e possa gerenciar centralmente a solução antimalware do console do Configuration Manager. 


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

  Julio executa as seguintes etapas para implementar o Endpoint Protection:  



##  <a name="steps-to-implement-endpoint-protection"></a>Etapas para implementar a proteção de ponto de extremidade  

|Processar|Referência|  
|-------------|---------------|  
|João analisa as informações disponíveis sobre os conceitos básicos do Endpoint Protection no Configuration Manager.|Para obter uma visão geral sobre o Endpoint Protection, consulte [Endpoint Protection no System Center Configuration Manager](endpoint-protection.md).|  
|João analisa e implementa os pré-requisitos necessários para usar o Endpoint Protection.|Para obter informações sobre os pré-requisitos do Endpoint Protection, consulte [Planejamento do Endpoint Protection](../plan-design/planning-for-endpoint-protection.md).|  
|João instala a função de sistema de sites do Endpoint Protection em apenas um servidor de sistema de sites, no topo da hierarquia do Banco Woodgrove.|Para obter mais informações sobre como instalar a função de sistema de sites do Endpoint Protection, veja os "Pré-requisitos" em [Configurar o Endpoint Protection](configure-endpoint-protection.md).|  
|João configura o Configuration Manager para usar um servidor SMTP para enviar alertas de email.<br /><br /> **Observação:** você precisará configurar um servidor SMTP somente se quiser ser notificado por email quando um alerta do Endpoint Protection for gerado.|Para obter mais informações, consulte [Configurar alertas no Endpoint Protection](endpoint-configure-alerts.md).|  
|João cria uma coleção de dispositivos que contém todos os computadores e servidores para instalar o cliente do Endpoint Protection. Ele chama a coleção de **Todos os computadores protegidos pelo Endpoint Protection**.<br /><br /> **Dica:** Você não pode configurar alertas para coleções de usuário.|Para obter mais informações sobre como criar coleções, consulte [Como criar coleções no System Center Configuration Manager](../../core/clients/manage/collections/create-collections.md)|  
|Ele configura os seguintes alertas para a coleção: <br /><br />1) **Malware detectado**: João configura a severidade do alerta como **Crítico**. <br /><br />2) **O mesmo tipo de malware é detectado em vários computadores**: Julio configura a severidade de alerta **Crítico** e especifica que o alerta será gerado quando mais de 5% dos computadores tiverem um malware detectado. <br /><br />3) **O mesmo tipo de malware é detectado repetidamente dentro do intervalo especificado em um computador**: Julio configura a severidade de alerta **Crítico** e especifica que o alerta será gerado quando um malware for detectado mais de 5 vezes em um período de 24 horas. <br /><br />4) **Vários tipos de malware são detectados no mesmo computador dentro do intervalo especificado**: Julio configura a severidade de alerta **Crítico** e especifica que o alerta será gerado quando mais de 3 tipos de malware forem gerados em um período de 24 horas.<br /><br /> O valor da **Severidade do Alerta** indica o nível de alerta que será exibido no console do Configuration Manager e nos alertas que ele receber uma mensagem de email.<br /><br /> Ele também seleciona a opção **Exibir esta coleção no painel do Endpoint Protection** para que possa monitorar os alertas no console do Configuration Manager.|Veja a seção “Configurar alertas para o Endpoint Protection” em [Configurando o Endpoint Protection no System Center Configuration Manager](endpoint-configure-alerts.md).|  
|João configura as atualizações de software do Configuration Manager para baixar e implantar atualizações de definição três vezes por dia usando uma regra de implantação automática.|Para obter mais informações, veja a seção "Usando as atualizações de Software do Configuration Manager para fornecer atualizações de definições" em [Usar atualizações de software do Configuration Manager para fornecer atualizações de definições](endpoint-definitions-configmgr.md).|  
|João examina as configurações na política de antimalware padrão, que contém as configurações de segurança da Microsoft. Para os computadores executarem uma verificação rápida diária, ele altera as configurações a seguir:<br /><br /> 1) **Executar uma verificação rápida diária nos computadores cliente**: **Sim**.<br /><br /> 2) **Hora de agendamento da verificação rápida diária**:  **09h00**.<br /><br /> João observa que as **atualizações distribuídas do Microsoft Update** são selecionadas por padrão como uma fonte de atualização de definição. Isso atende ao requisito de negócios de que os computadores baixem definições do Microsoft Update quando não puderem receber atualizações de software do Configuration Manager.|Consulte [Como criar e implantar políticas antimalware para o Endpoint Protection no System Center Configuration Manager](endpoint-antimalware-policies.md).|  
|João cria uma coleção que contém apenas os servidores do Woodgrove Bank chamada **Servidores do Woodgrove Bank**.|Consulte [Como criar coleções no System Center Configuration Manager](../../core/clients/manage/collections/create-collections.md)|  
|João cria uma política antimalware personalizada chamada **política de servidor do Woodgrove Bank**. Ele adiciona somente as configurações das **verificações agendadas** e faz as seguintes alterações:<br /><br /> **Tipo de verificação**:  **Completa**<br /><br /> **Dia da verificação**:  **Sábado**<br /><br /> **Hora da verificação**: **01h00**<br /><br /> **Executar uma verificação rápida diária nos computadores cliente**:  **Não**.|Consulte [Como criar e implantar políticas antimalware para o Endpoint Protection no System Center Configuration Manager](endpoint-antimalware-policies.md).|  
|João implanta a política personalizada antimalware chamada **Política de Servidor do Woodgrove Bank** na coleção **Servidores do Woodgrove Bank** .|Consulte "Para implantar uma política antimalware em computadores cliente" no artigo [Como criar e implantar políticas antimalware para o Endpoint Protection](endpoint-antimalware-policies.md).|  
|João cria um novo conjunto de configurações personalizadas de dispositivo do cliente para o Endpoint Protection e o denomina **Configurações do Endpoint Protection do Banco Woodgrove**.<br /><br /> **Observação:** se você não quiser instalar e habilitar o Endpoint Protection em todos os clientes de sua hierarquia, verifique se as opções **Gerenciar cliente do Endpoint Protection nos computadores cliente** e **Instalar o cliente do Endpoint Protection nos computadores cliente** foram definidas como **Não** nas configurações padrão do cliente.|Para obter mais informações, consulte [Definir configurações personalizadas do cliente para o Endpoint Protection](endpoint-protection-configure-client.md).|  
|Ele define as seguintes configurações para o Endpoint Protection:<br /><br /> **Gerenciar o cliente do Endpoint Protection em computadores cliente**:  **Sim**<br /><br /> A configuração e o valor garantem que qualquer cliente existente do Endpoint Protection que for instalado será gerenciado por Configuration Manager.<br /><br /> **Instalar o cliente do Endpoint Protection em computadores cliente**:  **Sim**.</br></br>**Observação** A partir do Configuration Manager 1802, os dispositivos Windows 10 não precisam ter o agente do Endpoint Protection instalado. Se ele já estiver instalado nos dispositivos Windows 10, o Configuration Manager não o removerá. Os administradores podem remover o agente do Endpoint Protection dos dispositivos Windows 10 que executam, no mínimo, a versão de cliente 1802.|Para obter mais informações, consulte [Definir configurações personalizadas do cliente para o Endpoint Protection](endpoint-protection-configure-client.md).|  
|João implanta as **Configurações do Endpoint Protection do Banco Woodgrove** do cliente na coleção **Todos os computadores protegidos pelo Endpoint Protection**.|Consulte “Definir configurações personalizadas do cliente para o Endpoint Protection” em [Configurando o Endpoint Protection no Configuration Manager](endpoint-antimalware-policies.md).|  
|João usa o assistente Criar Política de Firewall do Windows para criar uma política, definindo as seguintes configurações para o perfil de domínio:<br /><br /> 1) **Habilitar o Firewall do Windows**: **Sim**<br /><br /> 2)<br />                    **Notificar o usuário quando o Firewall do Windows bloquear um novo programa**: **Sim**|Consulte [Como criar e implantar políticas do Firewall do Windows para o Endpoint Protection no System Center Configuration Manager](../../protect/deploy-use/create-windows-firewall-policies.md)|  
|João implanta a nova política de firewall na coleção **Todos os computadores protegidos pelo Endpoint Protection** que criou anteriormente.|Consulte "Para implantar uma política de Firewall do Windows" em [Como criar e implantar políticas do Firewall do Windows para o Endpoint Protection no System Center Configuration Manager](create-windows-firewall-policies.md)|  
|João usa as tarefas de gerenciamento disponíveis para o Endpoint Protection para gerenciar políticas antimalware e do Firewall do Windows, executar varreduras sob demanda dos computadores quando necessário, forçar os computadores a baixarem as definições mais recentes e especificar uma ação adicional a ser tomada quando malware for detectado.|Consulte [Como gerenciar políticas antimalware e configurações de firewall para o Endpoint Protection no System Center Configuration Manager](endpoint-antimalware-firewall.md)|  
|João usa os seguintes métodos para monitorar o status do Endpoint Protection e as ações tomadas pelo Endpoint Protection:<br /><br /> 1) Usando o nó **Status do Endpoint Protection** em **Segurança** no workspace **Monitoramento**.<br /><br /> 2) Usar o nó o **Endpoint Protection** no workspace **Ativos e Conformidade**.<br /><br /> 3) Usar os relatórios internos do Configuration Manager.|Consulte [Como monitorar o Endpoint Protection no System Center Configuration Manager](monitor-endpoint-protection.md)|  

 João relata uma implementação bem-sucedida do Endpoint Protection ao seu gerente e confirma que os computadores do Banco Woodgrove estão protegidos contra malware, de acordo com os requisitos de negócios que ele recebeu.
