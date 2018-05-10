---
title: Cogerenciamento para dispositivos Windows 10
titleSuffix: Configuration Manager
description: Saiba como gerenciar dispositivos Windows 10 simultaneamente usando o Configuration Manager e o Microsoft Intune.
keywords: ''
author: mestew
ms.author: mstewart
manager: dougeby
ms.date: 03/28/2018
ms.topic: article
ms.prod: configuration-manager
ms.service: ''
ms.technology: ''
ms.assetid: d6bbc787-83a5-44b4-ad64-016e5da7413f
ms.openlocfilehash: 3d7ca4bb72f6f3f76855faac125385374347ba55
ms.sourcegitcommit: d67c6246bb6027cd5501e772b0521f9272407c28
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2018
---
# <a name="co-management-for-windows-10-devices"></a>Cogerenciamento para dispositivos Windows 10    
 Com atualizações anteriores do Windows 10, você pode associar um dispositivo com Windows 10 ao Active Directory (AD) local e ao Azure AD baseado em nuvem ao mesmo tempo (Azure AD híbrido). A partir do Configuration Manager versão 1710, o cogerenciamento usufrui dessa melhoria e permite gerenciar dispositivos Windows 10 versão 1709 simultaneamente usando o Configuration Manager e o Intune. <!-- 1350871 -->
## <a name="why-co-management"></a>Por que cogerenciamento?
Muitos clientes desejam gerenciar os dispositivos Windows 10 da mesma forma em que gerenciam os dispositivos móveis, usando uma solução baseada em nuvem simplificada e com menor custo. No entanto, fazer a transição do gerenciamento tradicional para o gerenciamento moderno pode ser um desafio.  
## <a name="what-is-co-management"></a>O que é cogerenciamento?
O cogerenciamento permite gerenciar dispositivos Windows 10 simultaneamente usando o Configuration Manager e o Intune. É uma solução que fornece uma ponte do gerenciamento tradicional para o moderno e fornece um caminho para fazer a transição usando uma abordagem em fases.

## <a name="benefits"></a>Benefícios 
- Uso imediato de recursos do Intune 
    - Ações remotas
        - [Redefinição de fábrica](https://docs.microsoft.com/intune/devices-wipe#factory-reset)
        - [Apagamento seletivo](https://docs.microsoft.com/intune/apps-selective-wipe)
        - [Excluir dispositivos](https://docs.microsoft.com/intune/devices-wipe#delete-devices-from-the-azure-active-directory-portal)
        - [Reiniciar dispositivo](https://docs.microsoft.com/intune/device-restart)
        - [Novo início](https://docs.microsoft.com/intune/device-fresh-start)
    - Orquestração com o Intune para as seguintes cargas de trabalho:
        - [Políticas de conformidade](https://docs.microsoft.com/intune/device-compliance-get-started)
        - [Políticas de acesso a recursos](https://docs.microsoft.com/intune/device-profiles)
        - [Políticas do Windows Update](https://docs.microsoft.com/intune/windows-update-for-business-configure)
        - [Endpoint Protection](https://docs.microsoft.com/en-us/intune/endpoint-protection-windows-10), a partir do Configuration Manager 1802. <!-- 1357365 -->
    
## <a name="how-to-configure-co-management"></a>Como configurar o cogerenciamento
Há dois caminhos principais para usar o cogerenciamento. Um é o cogerenciamento provisionado pelo Configuration Manager, no qual os dispositivos Windows 10 gerenciados pelo Configuration Manager e ingressados no Azure AD híbrido são registrados no Intune. O outro são os dispositivos provisionados pelo Intune que são registrados no Intune e, em seguida, são instalados com o cliente do Configuration Manager para atingir um estado de cogerenciamento.

### <a name="configuration-manager"></a>**Configuration Manager**
 -  Atualize para o Configuration Manager versão 1710 ou posterior.


### <a name="azure-active-directory"></a>**Azure Active Directory**
  - [Azure AD híbrido adicionado](https://docs.microsoft.com/azure/active-directory/device-management-hybrid-azuread-joined-devices-setup) (adicionado ao AD e ao Azure AD).
  - [Habilitar o registro automático no Windows 10.](https://docs.microsoft.com/intune/windows-enroll)


### <a name="intune"></a>**Intune**
 - [Como configurar a assinatura do Intune.](/sccm/mdm/deploy-use/configure-intune-subscription) ou https://docs.microsoft.com/en-us/intune/setup-steps
 - [Inicie a migração do MDM híbrido para o Intune autônomo.](/sccm/mdm/deploy-use/migrate-hybridmdm-to-intunesa)


### <a name="enable-co-management"></a>Habilitar cogerenciamento 
 No console do Configuration Manager, acesse **Administração** > **Visão Geral** > **Serviços de Nuvem** > **Cogerenciamento**. Escolha **Configurar o cogerenciamento** na faixa de opções para abrir o **Assistente para Integração de Cogerenciamento** 
   
1. Na página **Assinatura**, clique em **Entrar**, entre no seu locatário do Intune e, em seguida, clique em **Avançar**.    
2. Na página **Habilitação**, escolha sua configuração **Registro automático no Intune**. Copie a linha de comando para dispositivos já inscritos no Intune, se necessário. 
3. Na página **Cargas de Trabalho**, para cada carga de trabalho, escolha qual grupo de dispositivos mover para gerenciamento com o Intune.
4. Na página **Preparo**, selecione uma coleção de dispositivos para ser a **Coleção Piloto**. Verifique o **Resumo** e conclua o assistente. 

### <a name="upgrade-windows-10-client"></a>Atualizar o cliente do Windows 10
- Atualize para o [Windows 10, versão 1709 (também conhecido como a Atualização para Criadores) e posterior](/sccm/osd/deploy-use/manage-windows-as-a-service)

### <a name="configure-workloads-to-switch-to-intune"></a>Configurar cargas de trabalho para mudar para o Intune 
O artigo [Cargas de trabalho que podem ser transferidas para o Intune](/sccm/core/clients/manage/co-management-switch-workloads#Workloads-able-to-be-transitioned-to-Intune) mostra como mudar cargas de trabalho específicas do Configuration Manager para o Intune. O artigo também contém instruções sobre como alterar os grupos de dispositivos para os quais as cargas de trabalho são transferidas.

- **Políticas de conformidade:** As políticas de conformidade definem as regras e configurações que um dispositivo deve obedecer para ser considerado em conformidade pelas políticas de acesso condicional. Você também pode usar as políticas de conformidade para monitorar e corrigir problemas com dispositivos, independentemente do acesso condicional. Para obter detalhes, consulte [Políticas de conformidade do dispositivo](https://docs.microsoft.com/intune/device-compliance-get-started).  

- **Políticas do Windows Update:** As políticas do Windows Update for Business permitem configurar políticas de adiamento para atualizações de recursos ou atualizações de qualidade do Windows 10 para dispositivos Windows 10 gerenciados diretamente pelo Windows Update for Business. Para obter detalhes, consulte [Configurar as políticas de adiamento do Windows Update for Business](https://docs.microsoft.com/intune/windows-update-for-business-configure).  

- **Políticas de acesso a recursos:** as políticas de acesso a recursos definem as configurações de VPN, Wi-Fi, email e certificado nos dispositivos. Para obter detalhes, consulte [Implantar perfis de acesso a recursos](https://docs.microsoft.com/intune/device-profiles).

- **Endpoint Protection:** A partir do Configuration Manager 1802, a carga de trabalho do Endpoint Protection pode ser transferida para o Intune. Para saber mais, confira [Endpoint Protection para Microsoft Intune](https://docs.microsoft.com/en-us/intune/endpoint-protection-windows-10)<!-- 1357365 --> e [Cargas de trabalho que podem ser transferidas para o Intune](/sccm/core/clients/manage/co-management-switch-workloads#Workloads-able-to-be-transitioned-to-Intune)


### <a name="install-configuration-manager-client-to-the-devices-enrolled-in-intune"></a>Instalar o cliente do Configuration Manager nos dispositivos inscritos no Intune
Quando dispositivos Windows 10 são registrados no Intune, você pode instalar o cliente do Configuration Manager nos dispositivos ([usando um argumento de linha de comando específico](/sccm/core/clients/manage/co-management-prepare#command-line-to-install-configuration-manager-client)) para preparar os clientes para o cogerenciamento. Em seguida, você habilitar o cogerenciamento no console do Configuration Manager para começar a mover para o Intune cargas de trabalho específicas de dispositivos Windows 10 específicos.
Para dispositivos Windows 10 que ainda não estão registrados no Intune, você pode usar o registro automático no Azure para registrar os dispositivos. Para novos dispositivos Windows 10, você pode usar o [Windows AutoPilot](https://docs.microsoft.com/intune/enrollment-autopilot) para configurar a OOBE (configuração inicial pelo usuário), que inclui o registro automático de dispositivos no Intune.
 - Ative o [Gateway de Gerenciamento de Nuvem](/sccm/core/clients/manage/manage-clients-internet#cloud-management-gateway) no Configuration Manager (somente quando o Intune é usado para instalar o cliente do Configuration Manager).

## <a name="monitor-co-management"></a>Monitorar o cogerenciamento
[O painel do cogerenciamento](/sccm/core/clients/manage/co-management-dashboard) ajuda você a analisar os computadores cogerenciados no ambiente. Os gráficos podem ajudar a identificar os dispositivos que podem precisar de atenção.


## <a name="next-steps"></a>Próximas etapas
[Preparar dispositivos Windows 10 para cogerenciamento](co-management-prepare.md)
