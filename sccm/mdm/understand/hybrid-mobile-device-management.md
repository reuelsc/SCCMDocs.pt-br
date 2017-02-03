---
title: "MDM (Gerenciamento de Dispositivo Móvel) híbrido – Configuration Manager e Microsoft Intune | Microsoft Docs"
description: "Saiba mais sobre o MDM (gerenciamento de dispositivo móvel) híbrido com o System Center Configuration Manager e o Microsoft Intune."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: bb95154b-f63e-4491-896e-41d732c802f8
caps.latest.revision: 34
caps.handback.revision: 0
author: mtillman
ms.author: mtillman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 991eff171dce95590a7f050e0d3b07f98c0224b3
ms.openlocfilehash: ceeccab158cd23267ccd05cfbff82ef772f97fbc

---
# <a name="hybrid-mobile-device-management-mdm-with-system-center-configuration-manager-and-microsoft-intune"></a>MDM (gerenciamento de dispositivo móvel) híbrido com o System Center Configuration Manager e o Microsoft Intune

*Aplica-se a: System Center Configuration Manager (Branch Atual)*


É possível gerenciar dispositivos iOS, Windows e Android com o Configuration Manager e o Microsoft Intune. Todas as tarefas de gerenciamento são tratadas no console do Configuration Manager, em que você executa o restante de suas tarefas de gerenciamento de forma diretamente integrada ao serviço online do Microsoft Intune pela Internet.  É possível usar o Configuration Manager para permitir que os usuários acessem recursos da empresa em seus dispositivos de maneira segura e gerenciada. Usando o gerenciamento de dispositivos, você protege os dados da empresa enquanto permite que os usuários registrem dispositivos pessoais ou da empresa para acessar dados da empresa. Recursos de gerenciamento dos dispositivos:

-   Desativar e apagar dispositivos
-   Definir configurações de conformidade, como senhas, segurança, roaming, criptografia e comunicação sem fio
-   Implantar aplicativos de LOB (linha de negócios) em dispositivos
-   Implantar aplicativos em dispositivos que se conectam à Windows Store, Windows Phone Store, App Store ou Google Play
-   Coletar inventário de hardware
-   Coletar inventário de software usando relatórios internos

Para ler sobre os novos recursos que estão disponíveis para o MDM híbrido, consulte [What's new in hybrid mobile device management](../understand/whats-new-in-hybrid-mobile-device-management.md) (O que há de novo no gerenciamento de dispositivo móvel híbrido).

Este documento pressupõe que você esteja usando o Configuration Manager para gerenciar computadores, e que esteja interessado em estender o console do Configuration Manager com o Intune para gerenciar dispositivos móveis. Para entender as diferenças entre o Intune e gerenciamento de dispositivos móveis híbrido, consulte [Escolha entre o gerenciamento de dispositivo móvel híbrido e independente do Microsoft Intune com o System Center Configuration Manager](choose-between-standalone-intune-and-hybrid-mobile-device-management.md).

Após estender o Configuration Manager com o Intune, você pode registrar e gerenciar dispositivos corporativos ou conceder aos usuários permissão para registrar seus dispositivos pessoais. Você também pode gerenciar dispositivos corporativos com o Intune usando o Configuration Manager.

## <a name="hybrid-mdm-enrollment"></a>Registro no MDM híbrido
Para colocar dispositivos no gerenciamento híbrido, esses dispositivos devem estar registrados no serviço. A forma como os dispositivos são registrados depende do tipo de dispositivo, da propriedade e do nível de gerenciamento necessário. O registro de BYOD ("Traga seu próprio dispositivo") permite que os usuários registrem telefones, tablets ou PCs pessoais. O registro de COD (dispositivo corporativo) permite cenários de gerenciamento como apagamento remoto, dispositivos compartilhados ou afinidade de usuário para um dispositivo.

 Se usar o [Exchange ActiveSync](#mobile-device-management-with-exchange-activesync-and-configuration-manager), seja localmente ou hospedado na nuvem, você poderá habilitar o gerenciamento simples do Intune sem o registro. Computadores Windows também podem ser gerenciados usando o [Software cliente do Intune](/intune/deploy-use/manage-windows-pcs-with-microsoft-intune).

## <a name="overview-of-device-enrollment-methods"></a>Visão geral dos métodos de registro de dispositivo

 A tabela a seguir mostra os métodos de registro com e seus recursos com suporte. Esses recursos incluem:
 - **Apagar** – redefinir o dispositivo para as configurações de fábrica, removendo todos os dados. [Desativar dispositivos](../deploy-use/wipe-lock-reset-devices.md)
 - **Afinidade** – associa dispositivos a usuários. Necessário para MAM (gerenciamento de aplicativo móvel) e acesso condicional aos dados da empresa. [Afinidade do usuário](../deploy-use/user-affinity-for-hybrid-managed-devices.md)
 - **Bloqueio** – impede os usuários de removerem o dispositivo do gerenciamento. Dispositivos iOS exigem o modo Supervisionado para o Bloqueio. [Bloqueio remoto](../deploy-use/wipe-lock-reset-devices.md#remote-lock)

 **Métodos de registro do iOS**

| **Método** |  **Apagar** |  **Afinidade**    |   **Bloqueio** | **Detalhes** |
|:---:|:---:|:---:|:---:|:---:|
|**[BYOD](#byod)** | Não|    Sim |   Não | [mais](../deploy-use/setup-hybrid-mdm.md#step-6-enable-platform-enrollment)|
|**[DEM](#dem)**|   Não |Não |Não  | [mais](../deploy-use/enroll-devices-with-device-enrollment-manager.md)|
|**[DEP](#dep)**|   Sim |   Opcional |  Opcional|[mais](../deploy-use/ios-device-enrollment-program-for-hybrid.md)|
|**[USB-SA](#usb-sa)**| Sim |   Opcional |  Não| [mais](../deploy-use/ios-hybrid-enrollment-using-apple-configurator.md)|

**Métodos de registro do Android e do Windows**

| **Método** |  **Apagar** |  **Afinidade**    |   **Bloqueio** | **Detalhes**|
|:---:|:---:|:---:|:---:|:---:|:---:|
|**[BYOD](#byod)** | Não|    Sim |   Não | [mais](../deploy-use/setup-hybrid-mdm.md#windows-enrollment-setup)|
|**[DEM](#dem)**|   Não |Não |Não  |[mais](../deploy-use/enroll-devices-with-device-enrollment-manager.md)|

Para ver uma série de perguntas que ajudarão você a encontrar o método certo, consulte [Escolher como registrar dispositivos](/intune/get-started/choose-how-to-enroll-devices1).

## <a name="byod"></a>BYOD
Usuários de BYOD ("Traga seu próprio dispositivo") instalam o aplicativo de Portal da Empresa e registram o dispositivo. Isso pode permitir que os usuários se conectem à rede da empresa, ingressando no domínio ou no Azure Active Directory. Habilitar o registro de BYOD é um pré-requisito para muitos cenários de COD para a maioria das plataformas. Consulte [Configurar MDM híbrido](../deploy-use/setup-hybrid-mdm.md). ([Voltar à tabela](#overview-of-device-enrollment-methods))

## <a name="corporate-owned-devices"></a>Dispositivos corporativos
CODs (dispositivos corporativos) podem ser gerenciados com o console do Configuration Manager. Dispositivos iOS podem ser registrados diretamente por meio das ferramentas fornecidas pela Apple. Todos os tipos de dispositivo podem ser registrados por um administrador ou gerente usando o gerenciador de registro do dispositivo. Dispositivos que têm um número IMEI também podem ser identificados e marcados como corporativos para habilitar cenários de COD.

[Registrar dispositivos corporativos](../deploy-use/enroll-company-owned-devices.md)

### <a name="dem"></a>DEM
O gerenciador de registro de dispositivo é uma conta de usuário especial usada para registrar e gerenciar vários dispositivos corporativos. Os gerentes podem instalar o Portal da Empresa e registrar vários dispositivos sem usuário. Saiba mais sobre o [DEM](../deploy-use/enroll-devices-with-device-enrollment-manager.md). ([Voltar à tabela](#overview-of-device-enrollment-methods))

### <a name="dep"></a>DEP
O gerenciamento com o DEP (Programa de registro de dispositivos) da Apple permite criar e implantar políticas "por ondas de rádio" para dispositivos iOS adquiridos e gerenciados com o DEP. O dispositivo é registrado quando o usuário o ativa pela primeira vez e executa o Assistente de Configuração do iOS. Esse método dá suporte ao modo **iOS Supervisionado**, que por sua vez habilita:
   -    Registro bloqueado
   -    Acesso condicional
   -    Detecção de jailbreak
   -    Gerenciamento de aplicativos móveis

Saiba mais sobre o [DEP](../deploy-use/ios-device-enrollment-program-for-hybrid.md). ([Voltar à tabela](#overview-of-device-enrollment-methods))

### <a name="usb-sa"></a>USB-SA
Registro com Assistente de Configuração e conexão USB. O administrador cria uma política e a exporta para o Apple Configurator. Dispositivos corporativos conectados por USB são preparados com a política. O administrador deve registrar cada dispositivo manualmente. Os usuários recebem seus dispositivos e executam o Assistente de Configuração, registrando seu dispositivo. Esse método dá suporte ao modo **iOS Supervisionado**, que por sua vez habilita:
   -    Acesso condicional
   -    Detecção de jailbreak
   -    Gerenciamento de aplicativos móveis

Saiba mais sobre o [Registro com Assistente de Configuração com o Apple Configurator](../deploy-use/ios-hybrid-enrollment-using-apple-configurator.md). ([Voltar à tabela](#overview-of-device-enrollment-methods))

## <a name="mobile-device-management-with-exchange-activesync-and-configuration-manager"></a>Gerenciamento de dispositivo móvel usando o Exchange ActiveSync e o Configuration Manager
Dispositivos móveis que não estão registrados, mas que se conectam ao EAS (Exchange ActiveSync), podem ser gerenciados pelo Intune usando a política de MDM do EAS. O Intune usa o Exchange Connector para se comunicar com o EAS, tanto localmente quanto hospedado na nuvem.

[Gerenciamento de dispositivo móvel usando o Exchange ActiveSync e o Intune](../deploy-use/manage-mobile-devices-with-exchange-activesync.md)


##  <a name="supported-device-platforms"></a>Plataformas de dispositivos com suporte

O MDM híbrido do Configuration Manager pode gerenciar as seguintes plataformas de dispositivo:

[!INCLUDE[../includes/mdm-supported-devices](../includes/mdm-supported-devices.md)]

## <a name="next-steps"></a>Próximas etapas
 - [Pré-requisitos para o registro de dispositivos](../deploy-use/setup-hybrid-mdm.md)
 - [Gerenciar dispositivos corporativos](../deploy-use/enroll-company-owned-devices.md)



<!--HONumber=Jan17_HO4-->


