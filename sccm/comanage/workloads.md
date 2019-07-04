---
title: Cargas de trabalho de cogerenciamento
titleSuffix: Configuration Manager
description: Saiba mais sobre as cargas de trabalho que você pode mudar do Configuration Manager para o Microsoft Intune.
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 05/24/2019
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.assetid: 4c90befe-9c4e-4c27-a947-625887e15052
ms.collection: M365-identity-device-management
ms.openlocfilehash: 5fb11ac9ffbacfc37b69cb91d34a6885f44abe08
ms.sourcegitcommit: 3936b869d226cea41fa0090e2cbc92bd530db03a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/20/2019
ms.locfileid: "67286640"
---
# <a name="co-management-workloads"></a>Cargas de trabalho de cogerenciamento

Você não precisa mudar as cargas de trabalho, ou pode fazê-las individualmente quando estiver pronto. O Configuration Manager continua gerenciando todas as outras cargas de trabalho, incluindo as que você não mudar para o Intune e todos os outros recursos do Configuration Manager não compatíveis com cogerenciamento.

O cogerenciamento oferece suporte às seguintes cargas de trabalho:

- [Políticas de conformidade](#compliance-policies)  

- [Políticas do Windows Update](#windows-update-policies)  

- [Políticas de acesso a recursos](#resource-access-policies)  

- [Endpoint Protection](#endpoint-protection)  

- [Configuração do dispositivo](#device-configuration)  

- [Aplicativos Clique para Executar do Office](#office-click-to-run-apps)  

- [Aplicativos cliente](#client-apps)  


## <a name="compliance-policies"></a>Políticas de conformidade

As políticas de conformidade definem as regras e as configurações que um dispositivo deve cumprir para ser considerado em conformidade pelas políticas de acesso condicional. Também use políticas de conformidade para monitorar e corrigir problemas de conformidade com dispositivos independentemente do acesso condicional.

Para saber mais sobre o recurso do Intune, confira [Políticas de conformidade do dispositivo](https://docs.microsoft.com/intune/device-compliance-get-started).  


## <a name="windows-update-policies"></a>Políticas do Windows Update

As políticas do Windows Update para Empresas permitem configurar políticas de adiamento para atualizações de recursos ou atualizações de qualidade do Windows 10 para dispositivos Windows 10 gerenciados diretamente pelo Windows Update para Empresas.

Para saber mais sobre o recurso do Intune, confira [Configurar políticas de adiamento do Windows Update for Business](https://docs.microsoft.com/intune/windows-update-for-business-configure).  


## <a name="resource-access-policies"></a>Políticas de acesso a recursos

As políticas de acesso a recursos definem as configurações de VPN, Wi-Fi, email e certificado nos dispositivos.

Para saber mais sobre o recurso do Intune, confira [Implantar perfis de acesso a recursos](https://docs.microsoft.com/intune/device-profiles).

> [!Note]  
> A carga de trabalho de acesso do recurso também faz parte da configuração do dispositivo. Essas políticas são gerenciadas pelo Intune quando você muda a carga de trabalho de [Configuração do Dispositivo](#device-configuration).


## <a name="endpoint-protection"></a>Endpoint Protection

<!--1357365-->

A partir do Configuration Manager 1802, a carga de trabalho do Endpoint Protection inclui o pacote do Windows Defender de recursos de proteção contra malware:

- Windows Defender Antimalware
- Windows Defender Application Guard  
- Windows Defender Firewall  
- Windows Defender SmartScreen  
- Criptografia do Windows  
- Windows Defender Exploit Guard  
- Controle de Aplicativos do Windows Defender  
- Central de Segurança do Windows Defender  
- Proteção Avançada contra Ameaças do Windows Defender (agora conhecida como Proteção Avançada contra Ameaças do Microsoft Defender)
- Windows Information Protection  

Para saber mais sobre o recurso do Intune, confira [Endpoint Protection para Microsoft Intune](https://docs.microsoft.com/intune/endpoint-protection-windows-10).

> [!Note]  
> Quando você muda essa carga de trabalho, as políticas do Configuration Manager permanecem no dispositivo até serem substituídas pelas políticas do Intune. Esse comportamento garante que o dispositivo mantenha as políticas de proteção durante a transição.
>
> A carga de trabalho do Endpoint Protection também faz parte da configuração do dispositivo. O mesmo comportamento se aplica quando você muda a carga de trabalho de [Configuração do Dispositivo](#device-configuration).<!-- SCCMDocs.nl-nl issue #4 -->


## <a name="device-configuration"></a>Configuração do dispositivo

<!--1357903-->

A partir do Configuration Manager 1806, a carga de trabalho de configuração de dispositivo inclui configurações que você gerencia para os dispositivos da sua organização. A mudança dessa carga de trabalho também move as cargas de trabalho **Acesso de recurso** e **Endpoint Protection**.

Ainda é possível implantar as configurações do Configuration Manager em dispositivos cogerenciados mesmo que o Intune seja a autoridade de configuração do dispositivo. Essa exceção pode ser usada para definir configurações exigidas pela sua organização, mas ainda não disponíveis no Intune. Especifique essa exceção em uma [linha de base de configuração do Configuration Manager](/sccm/compliance/deploy-use/create-configuration-baselines). Ative a opção para **Sempre aplicar essa linha de base, mesmo para clientes cogerenciados**  ao criar a linha de base. Você pode alterá-la posteriormente na guia **Geral** das propriedades de uma linha de base existente.  

Para saber mais sobre o recurso do Intune, confira [Criar um perfil de dispositivo no Microsoft Intune](https://docs.microsoft.com/intune/device-profile-create).  


## <a name="office-click-to-run-apps"></a>Aplicativos Clique para Executar do Office

<!--1357841-->

A partir do Configuration Manager 1806, essa carga de trabalho gerencia aplicativos do Office 365 em dispositivos cogerenciados.

- Depois de mover a carga de trabalho, o aplicativo será exibido no **Portal da Empresa** no dispositivo  

- As atualizações do Office podem levar cerca de 24 horas para aparecer no cliente, a menos que os dispositivos sejam reiniciados  

- Há uma nova condição global, **Os aplicativos do Office 365 são gerenciados pelo Intune no dispositivo**. Essa condição é adicionada por padrão como um requisito dos novos aplicativos do Office 365. Ao fazer a transição dessa carga de trabalho, os clientes cogerenciados deixam de atender aos requisitos do aplicativo. Eles não instalam o Office 365 implantado por meio do Configuration Manager.  

Para saber mais sobre o recurso do Intune, confira [Atribuir aplicativos do Office 365 a dispositivos Windows 10 com o Microsoft Intune](https://docs.microsoft.com/intune/apps-add-office365).


## <a name="client-apps"></a>Aplicativos cliente

<!--1357892-->

A partir do Configuration Manager versão 1806, use o Intune para gerenciar aplicativos cliente e scripts do PowerShell em dispositivos Windows 10 cogerenciados. Após a transição dessa carga de trabalho, todos os aplicativos disponíveis implantados do Intune estão disponíveis no Portal da Empresa. Os aplicativos que você implanta do Configuration Manager estão disponíveis no Centro de Software.


Para saber mais sobre o recurso do Intune, confira [O que é o gerenciamento de aplicativo do Microsoft Intune?](https://docs.microsoft.com/intune/app-management).


> [!Note]  
> A carga de trabalho de aplicativos cliente é um recurso em pré-lançamento. Para habilitá-lo, veja [Recursos de pré-lançamento](/sccm/core/servers/manage/pre-release-features).  


## <a name="next-steps"></a>Próximas etapas

[Como mudar cargas de trabalho](/sccm/comanage/how-to-switch-workloads)  
