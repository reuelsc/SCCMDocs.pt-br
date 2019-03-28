---
title: Notificação de cliente
titleSuffix: Configuration Manager
description: Gerencie clientes executando ações imediatas de um console do Configuration Manager central.
ms.date: 03/19/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: deb8aac8-2bd9-4980-a25b-5f8d93051226
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 39135a1fa548c83e0ba9c7d2a98cf1e925217280
ms.sourcegitcommit: f38ef9afb0c608c0153230ff819e5f5e0fb1520c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/19/2019
ms.locfileid: "58197020"
---
# <a name="client-notification-in-configuration-manager"></a>Notificação do cliente no Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Para tomar uma ação imediata em clientes remotos, envie uma ação de notificação do cliente do console do Configuration Manager. Inicie essas ações em um dispositivo individual ou em uma coleção de dispositivos. 



## <a name="actions"></a>Ações

As seguintes ações estão na faixa de opções do grupo Dispositivos ou Coleções da guia Início. 


### <a name="install-client"></a>Cliente de instalação

Abre o **Assistente para Instalar Cliente**. O assistente usa a instalação do cliente por push para instalar um cliente do Configuration Manager. Para saber mais, confira [Instalação no cliente por push](/sccm/core/clients/deploy/deploy-clients-to-windows-computers#BKMK_ClientPush).

#### <a name="permissions"></a>Permissões
Esta ação exige as permissões **Modificar Recurso** e **Leitura** no objeto **Coleção**. 

As seguintes funções internas têm estas permissões por padrão:
- Administrador de Aplicativos  
- Administrador Completo  
- Administrador de Infraestrutura  
- Administrador de Operações  
- Gerenciador de Implantação do sistema operacional  

Adicione essas permissões a quaisquer funções personalizadas que precisem efetuar push ao cliente.


### <a name="run-script"></a>Executar Script

Abre o assistente **Executar Script** para executar um script do PowerShell em todos os clientes da coleção. Para saber mais, confira [Criar e executar scripts do PowerShell](/sccm/apps/deploy-use/create-deploy-scripts).

#### <a name="permissions"></a>Permissões
Esta ação exige a permissão **Executar Script** no objeto **Coleção**. 

As seguintes funções internas têm esta permissão por padrão:
- Administrador Completo  
- Administrador de Infraestrutura  
- Administrador de Operações  

Adicione essa permissão a quaisquer funções personalizadas que precisem executar scripts.


### <a name="start-cmpivot"></a>Iniciar o CMPivot

Inicia o **CMPivot**, que executa consultas em tempo real com relação aos dispositivos de destino. Para obter mais informações, veja [CMPivot](/sccm/core/servers/manage/cmpivot).

#### <a name="permissions"></a>Permissões
Esta ação exige as mesmas permissões que a ação [Executar script](#run-script). 



## <a name="client-notification"></a>Notificação de cliente

Essas ações estão no menu **Notificação do cliente**, na faixa de opções no grupo de Dispositivo ou Coleção da guia Início.

Na versão 1806 ou anterior, a opção **Notificação de Cliente** ficava disponível apenas no nó Coleção de Dispositivos ou ao exibir a associação de uma Coleção de Dispositivos. Já na versão 1810, é possível iniciar uma **Notificação de Cliente** diretamente do nó **Dispositivos**. Não é mais necessário estar dentro de uma exibição de associação de coleção. <!--SCCMDocs-pr issue 2972-->

#### <a name="permissions"></a>Permissões
<!--SCCMDocs-pr issue #2972-->
Da versão 1810 em diante, as ações de notificação do cliente agora exigem a permissão **Notificar Recurso** no objeto de Coleção. Essa permissão se aplica a todas as ações no menu **Notificação do cliente**. 

As seguintes funções internas têm esta permissão por padrão:
- Administrador Completo  
- Administrador de Infraestrutura  

Adicione essa permissão a quaisquer funções personalizadas que precisam usar ações de notificação do cliente.


### <a name="download-computer-policy"></a>Baixar a política de computador

Atualizar a política de dispositivo. Para obter mais informações, confira [Iniciar recuperação de política para um cliente do Configuration Manager](/sccm/core/clients/manage/manage-clients#BKMK_PolicyRetrieval).  


### <a name="download-user-policy"></a>Baixar a política de usuário

Atualizar a política de usuário.  


### <a name="collect-discovery-data"></a>Coletar dados de descoberta

Dispare clientes para enviar um DDR (registro de dados de descoberta). Para saber mais, confira [Descoberta de pulsação](/sccm/core/servers/deploy/configure/about-discovery-methods#bkmk_aboutHeartbeat).  


### <a name="collect-software-inventory"></a>Coletar inventário de software

Dispare clientes para executar um ciclo de inventário de software. Para obter mais informações, consulte [Introdução ao inventário de software](/sccm/core/clients/manage/inventory/introduction-to-software-inventory).  


### <a name="collect-hardware-inventory"></a>Coletar inventário de hardware

Dispare clientes para executar um ciclo de inventário de hardware. Para obter mais informações, consulte [Introdução ao inventário de hardware](/sccm/core/clients/manage/inventory/introduction-to-hardware-inventory).  


### <a name="evaluate-application-deployments"></a>Avaliar implantações de aplicativo

Dispare clientes para executar um ciclo de avaliação de implantação do aplicativo. Para saber mais, confira [Reavaliação de agendamento para implantações](/sccm/core/clients/deploy/about-client-settings#schedule-re-evaluation-for-deployments).  


### <a name="evaluate-software-update-deployments"></a>Avaliar implantações de atualização de software

Dispare clientes para executar um ciclo de avaliação de implantação de atualizações de software. Para saber mais, confira [Introdução às atualizações de software](/sccm/sum/understand/software-updates-introduction).  


### <a name="switch-to-the-next-software-update-point"></a>Alternar para o próximo ponto de atualização de software

Dispare clientes para alternar para o próximo ponto de atualização de software disponível. Para saber mais, confira [Mudança do ponto de atualização de software](/sccm/sum/plan-design/plan-for-software-updates#BKMK_SUPSwitching).  


### <a name="evaluate-device-health-attestation"></a>Avaliar o atestado de integridade do dispositivo

Dispare os clientes do Windows 10 para verificar e enviar o estado de integridade do dispositivo mais recente. Para obter mais informações, consulte [Atestado de integridade](/sccm/core/servers/manage/health-attestation).  


### <a name="check-conditional-access-compliance"></a>Verificar conformidade de acesso condicional

Dispare clientes para verificar a conformidade com acesso condicional. Para obter mais informações, confira [Gerenciar o acesso aos serviços do Office 365 para computadores](/sccm/mdm/deploy-use/manage-access-to-o365-services-for-pcs-managed-by-sccm).  


### <a name="wake-up"></a>Ativação

Da versão 1810 em diante, disparar dispositivos suspensos para que retornem ao estado de energia total.


### <a name="restart"></a>Reiniciar

Disparar os dispositivos selecionados para reiniciar. 



## <a name="endpoint-protection"></a>Endpoint Protection

As seguintes ações estão no menu **Endpoint Protection**. Este menu está na faixa de opções no grupo de Coleção da guia Início. Quando você seleciona um ou mais dispositivos, essas ações estão na guia **Objeto Selecionado** da faixa de opções.

Para obter mais informações, confira [Endpoint Protection no Configuration Manager](/sccm/protect/deploy-use/endpoint-protection).

#### <a name="permissions"></a>Permissões
Esta ação exige a permissão **Impor Segurança** no objeto **Coleção**. 

As seguintes funções internas têm esta permissão por padrão:
- Administrador Completo  
- Endpoint Protection Manager  
- Administrador de Operações  

Adicione essa permissão para quaisquer funções personalizadas que precisem disparar ações do Endpoint Protection.


### <a name="full-scan"></a>Verificação completa

Dispare o Endpoint Protection ou o Windows Defender para executar uma verificação antimalware *completa*.  


### <a name="quick-scan"></a>Verificação Rápida

Dispare Endpoint Protection ou Windows Defender para executar uma verificação antimalware *rápida*.  


### <a name="download-definition"></a>Baixar Definição

Dispare Endpoint Protection ou Windows Defender para baixar as definições antimalware mais recentes.  



## <a name="see-also"></a>Consulte também

- [Como gerenciar clientes](/sccm/core/clients/manage/manage-clients)
- [Como gerenciar coleções](/sccm/core/clients/manage/collections/manage-collections)
