---
title: 'Registrar dispositivos corporativos '
titleSuffix: Configuration Manager
description: Conheça os diferentes métodos para registrar dispositivos da empresa para implantações híbridas com o Configuration Manager.
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: e2754ce6-1460-4ddd-9050-2cc87e7964f4
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 36b4169f3bed1957f8ea14159902f408ba642944
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32346542"
---
# <a name="enroll-company-owned-devices-for-hybrid-deployments-with-configuration-manager"></a>Registrar dispositivos da empresa para implantações híbridas com o Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

COD (dispositivos de propriedade da empresa ou da organização) podem ser incluídos no gerenciamento de várias formas, dependendo do dispositivo e de como ele foi adquirido.  

## <a name="enroll-device-enrollment-program-ios-devices"></a>Registrar dispositivos iOS do Programa de Registro de Dispositivos  
 Implanta um perfil de registro "por ondas de rádio" para dispositivos adquiridos por meio do Programa de Registro de Dispositivo da Apple. Quando o usuário executa o Assistente de Configuração no dispositivo, ele é registrado no Intune.  Registros de dispositivos feitos pelo DEP não podem ser desfeitos pelos usuários. Consulte [Registro no DEP (Programa de Registro de Dispositivos) do iOS para implantações híbridas com o Configuration Manager](../../mdm/deploy-use/ios-device-enrollment-program-for-hybrid.md).  

## <a name="enroll-ios-devices-with-apple-configurator"></a>Registrar dispositivos iOS com o Apple Configurador  
 Este método requer que o administrador USB conecte o dispositivo iOS a um computador Mac que executa o Apple Configurator para pré-configurar o registro. Os dispositivos são então entregues aos usuários que executam o processo do Assistente de Configuração, configurando o dispositivo com suas credenciais corporativas ou de estudante e concluindo o processo de registro. Consulte [Registro híbrido do iOS usando o Apple Configurator com o Configuration Manager](../../mdm/deploy-use/ios-hybrid-enrollment-using-apple-configurator.md).  

## <a name="device-enrollment-manager"></a>Gerenciador de Registro de Dispositivos  
 As organizações podem usar o Intune para gerenciar um grande número de dispositivos móveis com uma única conta de usuário chamada de conta do gerente de registro de dispositivos. Depois de criar uma conta do gerenciador de registro de dispositivos, ela poderá ser usada por um gerente para registrar mais do que os cinco dispositivos padrão permitidos por padrão para usuários normais. Registrar dispositivos com uma conta de gerente de registro funciona somente para dispositivos que não são usados por um usuário específico. Esses dispositivos servem para pontos de vendas e aplicativos utilitários, por exemplo, mas não são indicados para usuários que precisam acessar os recursos ou o email da empresa. Consulte [Registrar dispositivos com o gerenciador de registro de dispositivo no Configuration Manager](../../mdm/deploy-use/enroll-devices-with-device-enrollment-manager.md).  

## <a name="user-affinity-for-managed-devices"></a>Afinidade de usuário para dispositivos gerenciados  
 Ao configurar perfis para dispositivos corporativos, o administrador pode especificar se os dispositivos gerenciados dão suporte à *afinidade de usuário*, que identifica um usuário específico com o dispositivo. Dispositivos configurados com **user affinity** podem instalar e executar o aplicativo de Portal da Empresa para baixar aplicativos e gerenciar dispositivos. Consulte [Afinidade de usuário para dispositivos híbridos gerenciados no Configuration Manager](../../mdm/deploy-use/user-affinity-for-hybrid-managed-devices.md).  

## <a name="manage-devices-with-activation-lock"></a>Gerenciar dispositivos com o Bloqueio de Ativação  
 O Microsoft Intune pode ajudar a gerenciar o Bloqueio de Ativação do iOS, um recurso do aplicativo Buscar meu iPhone para dispositivos iOS 7.1 e posterior. O Bloqueio de Ativação é habilitado automaticamente quando o aplicativo Buscar meu iPhone for usado em um dispositivo. Consulte [Gerenciar o Bloqueio de Ativação do iOS com o System Center Configuration Manager](../../mdm/deploy-use/manage-ios-activation-lock.md).

 ## <a name="predeclare-devices-with-imei-or-ios-serial-numbers"></a>Pré-declarar dispositivos com número de série do iOS ou IMEI

Você pode identificar os dispositivos corporativos importando seus números IMEI (identidade internacional de equipamento móvel) ou números de série do iOS. Você pode carregar um arquivo .csv (valores separados por vírgula) que contém os números IMEI do dispositivo ou inserir manualmente as informações sobre o dispositivo.  Consulte [Pré-declarar dispositivos com números de ID de hardware](../../mdm/deploy-use/predeclare-devices-with-hardware-id.md).
