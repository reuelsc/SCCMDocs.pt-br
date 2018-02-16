---
title: Cogerenciamento para dispositivos Windows 10
description: Saiba como gerenciar dispositivos Windows 10 simultaneamente usando o Configuration Manager e o Microsoft Intune.
keywords: 
author: dougeby
manager: angrobe
ms.date: 11/20/2017
ms.topic: article
ms.prod: configuration-manager
ms.service: 
ms.technology: 
ms.assetid: d6bbc787-83a5-44b4-ad64-016e5da7413f
ms.openlocfilehash: 0cc11a05013fd9c25ee98ec35adcbe822d8a21fb
ms.sourcegitcommit: 389c4e5b4e9953b74c13b1689195f99c526fa737
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/09/2018
---
# <a name="co-management-for-windows-10-devices"></a>Cogerenciamento para dispositivos Windows 10    
<!-- 1350871 -->
Muitos clientes desejam gerenciar os dispositivos Windows 10 da mesma forma em que gerenciam os dispositivos móveis, usando uma solução baseada em nuvem simplificada e com menor custo. No entanto, fazer a transição do gerenciamento tradicional para o gerenciamento moderno pode ser um desafio. Em atualizações anteriores do Windows 10, você pode associar um dispositivo com Windows 10 ao Active Directory (AD) local e ao Azure AD baseado em nuvem ao mesmo tempo (Azure AD híbrido). A partir do Configuration Manager versão 1710, o cogerenciamento usufrui dessa melhoria e permite gerenciar dispositivos Windows 10, versão 1709 (também conhecido como Fall Creators Update) simultaneamente usando o Configuration Manager e o Intune. É uma solução que fornece uma ponte do gerenciamento tradicional para o moderno e fornece um caminho para fazer a transição usando uma abordagem em fases. 

Há dois caminhos principais para usar o cogerenciamento.  Um é o cogerenciamento provisionado pelo Configuration Manager, no qual os dispositivos Windows 10 gerenciados pelo Configuration Manager e ingressados no Azure AD híbrido são registrados no Intune. O outro são os dispositivos provisionados pelo Intune que são registrados no Intune e, em seguida, são instalados com o cliente do Configuration Manager para atingir um estado de cogerenciamento.

## <a name="prerequisites"></a>Pré-requisitos
Você deve ter os seguintes pré-requisitos em vigor antes de habilitar o cogerenciamento. Há pré-requisitos gerais e pré-requisitos diferentes para dispositivos com o cliente do Configuration Manager e para dispositivos que não têm o cliente instalado.

> [!IMPORTANT]
> Dispositivos móveis Windows 10 não são compatíveis com o cogerenciamento.

### <a name="general-prerequisites"></a>Pré-requisitos gerais
Estes são os pré-requisitos gerais para habilitar o cogerenciamento:  

- Configuration Manager versão 1710 ou posterior
- Azure AD
- Licença do EMS ou do Intune para todos os usuários
- [Registro automático do Azure AD](https://docs.microsoft.com/intune/windows-enroll#enable-windows-10-automatic-enrollment) habilitado
- Assinatura do Intune &#40;autoridade do MDM no Intune definida para **Intune**&#41;


   > [!Note]  
   > Se você tiver um ambiente de MDM híbrido (Intune integrado ao Configuration Manager), não será possível habilitar o cogerenciamento. Se você estiver interessado em migrar para o Intune autônomo, consulte [Start migrating from hybrid MDM to Intune standalone](/sccm/mdm/deploy-use/migrate-hybridmdm-to-intunesa) (Iniciar a migração do MDM híbrido para o Intune autônomo).

### <a name="additional-prerequisites-for-devices-with-the-configuration-manager-client"></a>Pré-requisitos adicionais para dispositivos com o cliente do Configuration Manager
- Windows 10, versão 1709 (também conhecido como Fall Creators Update) e posterior
- [Azure AD híbrido ingressado](https://docs.microsoft.com/azure/active-directory/device-management-hybrid-azuread-joined-devices-setup) (ingressado no AD e ao Azure AD)

### <a name="additional-prerequisites-for-devices-without-the-configuration-manager-client"></a>Pré-requisitos adicionais para dispositivos sem o cliente do Configuration Manager
- Windows 10, versão 1709 (também conhecido como Fall Creators Update) e posterior
- [Gateway de Gerenciamento de Nuvem](/sccm/core/clients/manage/manage-clients-internet#cloud-management-gateway) no Configuration Manager (quando o Intune é usado para instalar o cliente do Configuration Manager)

## <a name="workloads-you-can-switch-to-intune"></a>Cargas de trabalho que você pode mudar para o Intune
Depois que você habilitar o cogerenciamento, o Configuration Manager continuará a gerenciar todas as cargas de trabalho. Quando você decidir que está pronto, poderá fazer com que o Intune comece a gerenciar as cargas de trabalho disponíveis. Você pode fazer com que o Intune gerencie as cargas de trabalho as seguir.   

### <a name="compliance-policies"></a>Políticas de conformidade
As políticas de conformidade definem as regras e configurações que um dispositivo deve obedecer para ser considerado em conformidade pelas políticas de acesso condicional. Você também pode usar as políticas de conformidade para monitorar e corrigir problemas com dispositivos, independentemente do acesso condicional. Para obter detalhes, consulte [Políticas de conformidade do dispositivo](/sccm/mdm/deploy-use/device-compliance-policies).  

### <a name="windows-update-for-business-policies"></a>Políticas do Windows Update para Empresas
As políticas do Windows Update para Empresas permitem configurar políticas de adiamento para atualizações de recursos ou atualizações de qualidade do Windows 10 para dispositivos Windows 10 gerenciados diretamente pelo Windows Update para Empresas. Para obter detalhes, consulte [Configurar as políticas de adiamento do Windows Update for Business](/sccm/sum/deploy-use/integrate-windows-update-for-business-windows-10#configure-windows-update-for-business-deferral-policies).  

### <a name="resource-access-policies"></a>Políticas de acesso a recursos
As políticas de acesso a recursos definem as configurações de VPN, Wi-Fi, email e certificado nos dispositivos. Para obter detalhes, consulte [Implantar perfis de acesso a recursos](/sccm/protect/deploy-use/deploy-wifi-vpn-email-cert-profiles).

## <a name="architectural-overview-for-co-management"></a>Visão geral de arquitetura para cogerenciamento
O diagrama a seguir fornece uma visão geral da arquitetura de cogerenciamento e como ela se encaixa nas infraestruturas existentes do Configuration e do Intune.

![Diagrama de arquitetura de cogerenciamento](./media/co-management-arch.svg)

## <a name="scenarios-to-enable-co-management"></a>Cenários para habilitar o cogerenciamento  
Você pode habilitar o cogerenciamento tanto para dispositivos Windows 10 registrados no Microsoft Intune quanto para clientes Windows 10 existentes do Configuration Manager. Ambos os cenários resultam em dispositivos Windows 10 gerenciados simultaneamente pelo Configuration Manager e pelo Intune, e também ingressados no AD e no Azure AD.  

### <a name="devices-enrolled-in-intune"></a>Dispositivos registrados no Intune  
Quando dispositivos Windows 10 são registrados no Intune, você pode instalar o cliente do Configuration Manager nos dispositivos (usando um argumento de linha de comando específico) para preparar os clientes para o cogerenciamento. Em seguida, você habilitar o cogerenciamento no console do Configuration Manager para começar a mover para o Intune cargas de trabalho específicas de dispositivos Windows 10 específicos.  

Para dispositivos Windows 10 que ainda não estão registrados no Intune, você pode usar o registro automático no Azure para registrar os dispositivos. Para novos dispositivos Windows 10, você pode usar o [Windows AutoPilot](https://docs.microsoft.com/intune/enrollment-autopilot) para configurar a OOBE (configuração inicial pelo usuário), que inclui o registro automático de dispositivos no Intune.  

### <a name="configuration-manager-clients"></a>Clientes do Configuration Manager
Quando houver dispositivos Windows 10 que sejam clientes do Configuration Manager, você poderá registrar esses dispositivos e habilitar o cogerenciamento no console do Configuration Manager. O Configuration Manager dispara o registro automático no Intune com base nas informações de locatário do Azure AD.  


## <a name="remote-actions-available-in-intune-on-azure-for-co-managed-devices"></a>Ações remotas disponíveis no Intune no Azure para dispositivos cogerenciados
Quando um dispositivo Windows 10 está habilitado para cogerenciamento, você tem as seguintes ações remotas disponíveis por meio do Intune no Azure:  
- [Redefinição de fábrica](https://docs.microsoft.com/intune/devices-wipe#factory-reset)
- [Apagamento seletivo](https://docs.microsoft.com/intune/apps-selective-wipe)
- [Excluir dispositivos](https://docs.microsoft.com/intune/devices-wipe#delete-devices-from-the-azure-active-directory-portal)
- [Reiniciar dispositivo](https://docs.microsoft.com/intune/device-restart)
- [Novo início](https://docs.microsoft.com/intune/device-fresh-start)

## <a name="next-steps"></a>Próximas etapas
[Preparar dispositivos Windows 10 para cogerenciamento](co-management-prepare.md)