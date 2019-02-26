---
title: Cargas de trabalho de cogerenciamento
titleSuffix: Configuration Manager
description: Saiba mais sobre as cargas de trabalho que você pode alternar do Configuration Manager para o Microsoft Intune.
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 01/14/2019
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.assetid: 4c90befe-9c4e-4c27-a947-625887e15052
ms.collection: M365-identity-device-management
ms.openlocfilehash: a3723595091e57a7ad2267a4da325e7c134c7bf1
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56754540"
---
# <a name="co-management-workloads"></a>Cargas de trabalho de cogerenciamento

Você não precise mudar as cargas de trabalho, ou você pode fazê-las individualmente, quando você estiver pronto. Configuration Manager continua a gerenciar todas as outras cargas de trabalho, incluindo cargas de trabalho que você não mudar para o Intune e não dá suporte a todos os outros recursos do Configuration Manager que cogerenciamento.

Cogerenciamento oferece suporte aos seguintes cargas de trabalho:

- [Políticas de conformidade](#compliance-policies)  

- [Políticas do Windows Update](#windows-update-policies)  

- [Políticas de acesso a recursos](#resource-access-policies)  

- [Endpoint Protection](#endpoint-protection)  

- [Configuração do dispositivo](#device-configuration)  

- [Clique para executar os aplicativos do Office](#office-click-to-run-apps)  

- [Aplicativos cliente](#client-apps)  



## <a name="compliance-policies"></a>Políticas de conformidade 

As políticas de conformidade definem as regras e as configurações que um dispositivo deve cumprir para ser considerado em conformidade pelas políticas de acesso condicional. Também use políticas de conformidade para monitorar e corrigir problemas de conformidade com dispositivos independentemente do acesso condicional. 

Para obter mais informações sobre o recurso do Intune, consulte [políticas de conformidade do dispositivo](https://docs.microsoft.com/intune/device-compliance-get-started).  



## <a name="windows-update-policies"></a>Políticas do Windows Update

As políticas do Windows Update para Empresas permitem configurar políticas de adiamento para atualizações de recursos ou atualizações de qualidade do Windows 10 para dispositivos Windows 10 gerenciados diretamente pelo Windows Update para Empresas. 

Para obter mais informações sobre o recurso do Intune, consulte [configurar o Windows Update para políticas de adiamento de negócios](https://docs.microsoft.com/intune/windows-update-for-business-configure).  



## <a name="resource-access-policies"></a>Políticas de acesso a recursos

As políticas de acesso a recursos definem as configurações de VPN, Wi-Fi, email e certificado nos dispositivos. 

Para obter mais informações sobre o recurso do Intune, consulte [implantar perfis de acesso de recurso](https://docs.microsoft.com/intune/device-profiles).



## <a name="endpoint-protection"></a>Endpoint Protection
<!--1357365-->

A partir do Configuration Manager 1802, a carga de trabalho do Endpoint Protection inclui o pacote do Windows Defender de recursos de proteção de antimalware: 

- Windows Defender Application Guard  
- Windows Defender Firewall  
- Windows Defender SmartScreen  
- Criptografia do Windows  
- Windows Defender Exploit Guard  
- Controle de Aplicativos do Windows Defender  
- Central de Segurança do Windows Defender  
- Proteção Avançada contra Ameaças do Windows Defender  
- Windows Information Protection  

Para obter mais informações sobre o recurso do Intune, consulte [Endpoint Protection do Microsoft Intune](https://docs.microsoft.com/intune/endpoint-protection-windows-10).



## <a name="device-configuration"></a>Configuração do dispositivo
<!--1357903-->

A partir do Configuration Manager 1806, a carga de trabalho de configuração de dispositivo inclui configurações que você gerencia dispositivos em sua organização. Alternar essa carga de trabalho também move os **acesso a recursos** e **Endpoint Protection** cargas de trabalho.

Ainda é possível implantar as configurações do Configuration Manager em dispositivos cogerenciados mesmo que o Intune seja a autoridade de configuração do dispositivo. Essa exceção pode ser usada para definir as configurações que sua organização precisa, mas ainda não estão disponível no Intune. Especifique essa exceção em uma [linha de base de configuração do Configuration Manager](/sccm/compliance/deploy-use/create-configuration-baselines). Habilite a opção para **sempre Aplique esta linha de base, mesmo para os clientes gerenciados em conjunto** ao criar a linha de base. Você pode alterá-lo posteriormente a **geral** guia das propriedades de uma linha de base existente.  

Para obter mais informações sobre o recurso do Intune, consulte [criar um perfil de dispositivo no Microsoft Intune](https://docs.microsoft.com/intune/device-profile-create).  



## <a name="office-click-to-run-apps"></a>Aplicativos Clique para Executar do Office
<!--1357841-->

A partir do Configuration Manager 1806, essa carga de trabalho gerencia aplicativos do Office 365 em dispositivos gerenciados em conjunto. 

- Depois de mover a carga de trabalho, o aplicativo será exibido no **Portal da Empresa** no dispositivo  

- As atualizações do Office podem levar cerca de 24 horas para aparecer no cliente, a menos que os dispositivos sejam reiniciados  

- Há uma nova condição global, **Os aplicativos do Office 365 são gerenciados pelo Intune no dispositivo**. Essa condição é adicionada por padrão como um requisito dos novos aplicativos do Office 365. Ao fazer a transição dessa carga de trabalho, os clientes cogerenciados deixam de atender aos requisitos do aplicativo. Eles não instalam o Office 365 implantado por meio do Configuration Manager.  

Para obter mais informações sobre o recurso do Intune, consulte [aplicativos de atribuir o Office 365 para dispositivos Windows 10 com o Microsoft Intune](https://docs.microsoft.com/intune/apps-add-office365). 



## <a name="client-apps"></a>Aplicativos cliente
<!--1357892-->

A partir do Configuration Manager versão 1806, use o Intune para gerenciar aplicativos de cliente em dispositivos Windows 10 cogerenciados. Após a transição dessa carga de trabalho, todos os aplicativos disponíveis implantados do Intune estão disponíveis no Portal da Empresa. Os aplicativos que você implanta do Configuration Manager estão disponíveis no Centro de Software.

Para obter mais informações sobre o recurso do Intune, consulte [o que é gerenciamento de aplicativo do Microsoft Intune?](https://docs.microsoft.com/intune/app-management). 

> [!Note]  
> A carga de trabalho de aplicativos de cliente é um recurso de pré-lançamento. Para habilitá-lo, veja [Recursos de pré-lançamento](/sccm/core/servers/manage/pre-release-features).  



## <a name="next-steps"></a>Próximas etapas

[Como mudar cargas de trabalho](/sccm/comanage/how-to-switch-workloads)  


