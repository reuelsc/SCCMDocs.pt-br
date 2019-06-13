---
title: Como fechar sua conta
titleSuffix: Configuration Manager
description: Como remover a área de trabalho de análise de sua conta do Azure
ms.date: 06/11/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 6e7d2850-b0af-497e-bbc1-bfc2a7420a7a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.collection: M365-identity-device-management
ms.openlocfilehash: 499d24e20b8220e685cb7aed9adea3f21caa12ae
ms.sourcegitcommit: e3c1eb0b75d79c05a750d49354c851d15d5e26a3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/13/2019
ms.locfileid: "67039737"
---
# <a name="how-to-close-your-account"></a>Como fechar sua conta

> [!Note]  
> Essas informações se relaciona a um serviço de visualização que pode ser substancialmente modificado antes do lançamento comercial. A Microsoft não oferece garantias, expressas ou implícitas, quanto às informações fornecidas aqui.  

Se você configurar a análise de área de trabalho em seu ambiente e, em seguida, decide que precisa removê-lo, use esse processo para fechar sua conta.

## <a name="contact-support"></a>Contate o suporte

A primeira etapa é entrar em contato com o Microsoft Support. Abra um caso de suporte para fechar sua conta da análise de área de trabalho. Não continue com as etapas adicionais até que você recebe a confirmação de que a Microsoft fechado sua conta.

## <a name="delete-the-solution"></a>Excluir a solução

1. Entrar para o [portal do Azure](https://portal.azure.com) como um usuário com o **administrador de empresa** função.

1. Pesquisar na **todos os recursos** para o nome do seu espaço de trabalho de análise de área de trabalho. Esse nome é o que você criou quando você se inscrever para o serviço.

1. Exclua `Microsoft365Analytics(YourWorkspaceName)` do tipo **solução**.

Os dados da área de trabalho de análise seja desativado com base em sua política de retenção de dados para o espaço de trabalho. Você pode continuar usando outras soluções no mesmo espaço de trabalho.

> [!Important]  
> Se você estiver usando o espaço de trabalho do Log Analytics com outras soluções, como o Windows Analytics, não exclua o espaço de trabalho.

## <a name="remove-user-and-app-access"></a>Remover o acesso de usuário e aplicativo

1. Entrar para o [portal do Azure](https://portal.azure.com) como um usuário com o **administrador de empresa** função. Vá para **do Azure Active Directory**.

1. Na **funções e os administradores**, pesquise o **administrador da área de trabalho de análise** função. Remova seus membros.

1. Na **grupos**, remover os membros dos grupos a seguir:

    - **M365 Os administradores do cliente de análise (proprietários de análise de Log)**
    - **M365 Os administradores do cliente de análise (colaboradores de análise de Log)**

1. Na **aplicativos empresariais**, excluir ou revogar permissões de acesso para os seguintes aplicativos:

    - `MaLogAnalyticsReader`

    - O aplicativo do ConfigMgr. Para localizar o nome desse aplicativo, vá para o console do Configuration Manager. No **administração** espaço de trabalho, expanda **serviços de nuvem**e selecione o **serviços do Azure** nó. Abra as propriedades do **análise de área de trabalho** de serviço e, em seguida, alterne para o **aplicativos** guia. O **aplicativo Web** é este aplicativo do Azure.

        > [!Important]  
        > Antes de fazer alterações a esse aplicativo no Azure AD, certifique-se de que você não estiver reutilizá-lo com outro serviço no Configuration Manager.

## <a name="disconnect-configuration-manager"></a>Desconectar do Configuration Manager

1. Abra o console do Configuration Manager como um usuário com o **administrador completo** função.

1. Vá para o **Administration** espaço de trabalho, expanda **serviços de nuvem**e selecione o **serviços do Azure** nó.

1. Exclua o serviço de análise de área de trabalho.

## <a name="reconfigure-clients"></a>Reconfigurar os clientes

### <a name="unenroll-devices"></a>Cancelar o registro de dispositivos

Em dispositivos registrados, remova o valor de CommercialID dos seguintes chaves do registro do Windows:

- `HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\DataCollection`
- `HKLM:\SOFTWARE\Policies\Microsoft\Windows\DataCollection`

### <a name="windows-diagnostic-data-configuration"></a>Configuração de dados de diagnóstico do Windows

Se não quiser que os dispositivos para continuar a enviar dados de diagnóstico:

- Windows 10: definir o nível de dados de diagnóstico para **segurança**
- Windows 7 SP1 ou 8.1: desabilitar o **dados comerciais no consentimento chave**

Defina esses valores usando um dos seguintes métodos:

- A diretiva de grupo, na **configuração do computador** > **modelos administrativos** > **componentes do Windows**  >  **Coleta de dados e compilações de visualização**
- Gerenciamento de dispositivo móvel (MDM), tais como [Microsoft Intune](https://docs.microsoft.com/intune/device-restrictions-windows-10#reporting-and-telemetry)

Para saber mais, veja [Configurar dados de diagnóstico do Windows em sua organização](https://docs.microsoft.com/windows/privacy/configure-windows-diagnostic-data-in-your-organization).

> [!NOTE]  
> Quando você aplica essas alterações, dispositivos imediatamente parar de enviar dados de diagnóstico. Pode levar 24 a 48 horas para a Microsoft parar o processamento de insights para seu espaço de trabalho. Microsoft exclui esses dados de seus serviços de nuvem dentro de 30 dias ou menos.
