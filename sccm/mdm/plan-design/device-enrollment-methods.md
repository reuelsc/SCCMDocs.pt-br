---
title: Métodos de registro de dispositivo para MDM híbrido
titleSuffix: Configuration Manager
description: Métodos de registro de dispositivo para MDM híbrido.
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: b81d06dc-3844-4117-9937-16732a227994
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 89501e22c855f31264fbf94fe093d8ebde08708f
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="overview-of-device-enrollment-methods"></a>Visão geral dos métodos de registro de dispositivo

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Após estender o Configuration Manager com o Intune, você pode registrar e gerenciar dispositivos corporativos ou conceder aos usuários permissão para registrar seus dispositivos pessoais. Você também pode gerenciar dispositivos corporativos com o Intune usando o Configuration Manager.

A tabela a seguir mostra os métodos de registro com e seus recursos com suporte. Esses recursos incluem:
- **Apagar** – redefinir o dispositivo para as configurações de fábrica, removendo todos os dados. [Desativar dispositivos](../deploy-use/wipe-lock-reset-devices.md)
- **Afinidade** – associa dispositivos a usuários. Necessário para MAM (gerenciamento de aplicativo móvel) e acesso condicional aos dados da empresa. [Afinidade do usuário](../deploy-use/user-affinity-for-hybrid-managed-devices.md)
- **Bloqueio** – impede os usuários de removerem o dispositivo do gerenciamento. Dispositivos iOS exigem o modo Supervisionado para o Bloqueio. [Bloqueio remoto](../deploy-use/wipe-lock-reset-devices.md#remote-lock)

**Métodos de registro do iOS**

| **Método** |  **Apagar** |  **Afinidade**    |   **Bloqueio** | **Detalhes** |
|:---:|:---:|:---:|:---:|:---:|
|**[BYOD](#byod)** | Não|    Sim |   Não | [mais](../deploy-use/enable-platform-enrollment.md)|
|**[DEM](#dem)**|   Não |Não |Não  | [mais](../deploy-use/enroll-devices-with-device-enrollment-manager.md)|
|**[DEP](#dep)**|   Sim |   Opcional |  Opcional|[mais](../deploy-use/ios-device-enrollment-program-for-hybrid.md)|
|**[USB-SA](#usb-sa)**| Sim |   Opcional |  Não| [mais](../deploy-use/ios-hybrid-enrollment-using-apple-configurator.md)|

**Métodos de registro do Android e do Windows**

| **Método** |  **Apagar** |  **Afinidade**    |   **Bloqueio** | **Detalhes**|
|:---:|:---:|:---:|:---:|:---:|:---:|
|**[BYOD](#byod)** | Não|    Sim |   Não | [mais](../deploy-use/enroll-hybrid-windows.md)|
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
  - Registro bloqueado
  - Acesso condicional
  - Detecção de jailbreak
  - Gerenciamento de aplicativos móveis

Saiba mais sobre o [DEP](../deploy-use/ios-device-enrollment-program-for-hybrid.md). ([Voltar à tabela](#overview-of-device-enrollment-methods))

### <a name="usb-sa"></a>USB-SA
Registro com Assistente de Configuração e conexão USB. O administrador cria uma política e a exporta para o Apple Configurator. Dispositivos corporativos conectados por USB são preparados com a política. O administrador deve registrar cada dispositivo manualmente. Os usuários recebem seus dispositivos e executam o Assistente de Configuração, registrando seu dispositivo. Esse método dá suporte ao modo **iOS Supervisionado**, que por sua vez habilita:
  - Acesso condicional
  - Detecção de jailbreak
  - Gerenciamento de aplicativos móveis

Saiba mais sobre o [Registro com Assistente de Configuração com o Apple Configurator](../deploy-use/ios-hybrid-enrollment-using-apple-configurator.md). ([Voltar à tabela](#overview-of-device-enrollment-methods))

## <a name="mobile-device-management-with-exchange-activesync-and-configuration-manager"></a>Gerenciamento de dispositivo móvel usando o Exchange ActiveSync e o Configuration Manager
Dispositivos móveis que não estão registrados, mas que se conectam ao EAS (Exchange ActiveSync), podem ser gerenciados pelo Intune usando a política de MDM do EAS. O Intune usa o Exchange Connector para se comunicar com o EAS, tanto localmente quanto hospedado na nuvem.

[Gerenciamento de dispositivo móvel usando o Exchange ActiveSync e o Intune](../deploy-use/manage-mobile-devices-with-exchange-activesync.md)
