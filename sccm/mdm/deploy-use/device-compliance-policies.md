---
title: Políticas de conformidade do dispositivo
titleSuffix: Configuration Manager
description: Saiba como gerenciar as políticas de conformidade no Configuration Manager para tornar aos dispositivos em conformidade políticas de acesso condicional.
ms.date: 03/19/2019
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: ad8fa94d-45bb-4c94-8d86-31234c5cf21c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 4e225b7ab54a1061387d1c8ee369641f68bd7889
ms.sourcegitcommit: f38ef9afb0c608c0153230ff819e5f5e0fb1520c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/19/2019
ms.locfileid: "58196867"
---
# <a name="device-compliance-policies-in-system-center-configuration-manager"></a>Políticas de conformidade de dispositivo no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

As políticas de conformidade no Configuration Manager definem as regras e configurações às quais um dispositivo deve obedecer para ser considerado em conformidade segundo as políticas de acesso condicional. Você também pode usar as políticas de conformidade para monitorar e corrigir problemas com dispositivos, independentemente do acesso condicional.  


> [!IMPORTANT]  
>  Este artigo descreve as políticas de conformidade para dispositivos gerenciados pelo Microsoft Intune. As políticas de conformidade para dispositivos gerenciados pelo cliente do Configuration Manager é descrito em [gerenciar o acesso aos serviços do Office 365 para dispositivos gerenciados pelo Configuration Manager](/sccm/protect/deploy-use/manage-access-to-o365-services-for-pcs-managed-by-sccm).  

 Essas regras incluem requisitos, como:  

-   PIN e senhas para acessar um dispositivo  

-   Criptografia dos dados armazenados no dispositivo  

-   Se o dispositivo está desbloqueado ou com raiz  

-   Se o email no dispositivo é gerenciado por uma política do Intune ou se o dispositivo é relatado como não íntegro pelo serviço de atestado de integridade de dispositivo do Windows.  

-   Aplicativos que não podem ser instalados no dispositivo.  


 Implante políticas de conformidade em coleções de usuários. Quando uma política de conformidade é implantada para um usuário, todos os dispositivos de usuários são verificados quanto à conformidade.  



## <a name="supported-device-types"></a>Tipos de dispositivo compatíveis

 A tabela a seguir lista os tipos de dispositivos compatíveis com as políticas de conformidade e como configurações não compatíveis são gerenciadas quando a política é usada com uma política de acesso condicional.  

|Regra|Windows 8.1 e posterior|Windows Phone 8.1 e posterior|iOS 6.0 e posterior|Android 4.0 e posterior ou Samsung KNOX Standard 4.0 e posterior, Android for Work|  
|----------|---------------------------|---------------------------------|-----------------------|---------------------------|-----------------------------------------|  
|**Configuração de senha ou PIN**|Corrigida|Corrigida|Corrigida|Em Quarentena|  
|**Criptografia de dispositivo**|N/D|Corrigida|Corrigida (pela definição do PIN)|Em Quarentena<br>(Android for Work sempre criptografado)|  
|**Dispositivo com jailbreak ou root**|N/D|N/D|Em Quarentena (não é uma configuração)|Em Quarentena (não é uma configuração)|  
|**Perfil de email**|N/D|N/D|Em Quarentena|N/D|  
|**Versão mínima do SO**|Em Quarentena|Em Quarentena|Em Quarentena|Em Quarentena|  
|**Versão máxima do SO**|Em Quarentena|Em Quarentena|Em Quarentena|Em Quarentena|  
|**Atestado de Integridade do Dispositivo (atualização 1602)**|A configuração não é aplicável ao Windows 8.1<br /><br /> O Windows 10 e o Windows 10 Mobile estão em quarentena.|N/D|N/D|N/D|  
|**Aplicativos que não podem ser instalados**|N/D|N/D|Em Quarentena|Em Quarentena|

 **Corrigidas** = a conformidade é imposta pelo sistema operacional do dispositivo. Por exemplo, o usuário é forçado a definir um PIN. Nunca há um caso em que a configuração está em não conformidade.  

 **Em quarentena** = o sistema operacional do dispositivo não impõe a conformidade. Por exemplo, dispositivos Android não forçam o usuário a criptografar o dispositivo. Nesse caso:  

-   Se o usuário for afetado pela política de acesso condicional, o dispositivo será bloqueado.  

-   O portal da empresa ou um portal da Web notifica o usuário sobre quaisquer problemas de conformidade.  



## <a name="devices-without-any-assigned-compliance-policy"></a>Dispositivos sem nenhuma política de conformidade atribuída
<!--2520152-->
A partir de julho de 2018, configure se todos os dispositivos que não tem nenhuma política de conformidade atribuída são considerados em conformidade ou fora de conformidade. Por padrão, os dispositivos sem política de conformidade atribuída são considerados em conformidade. Use as etapas a seguir para alterar essa configuração no portal do Azure:

1. Entrar no [Intune no portal do Azure](https://aka.ms/intuneportal).  

2. Selecione **Conformidade do dispositivo** e, em seguida, selecione **Configurações de política de conformidade** no grupo de Configuração.  

3. Na configuração **Marque os dispositivos sem nenhuma política de conformidade atribuída como**, selecione uma das seguintes opções:  

     - **Em conformidade** (padrão) – os dispositivos sem política de conformidade atribuída são considerados em conformidade com a política. Se o acesso condicional estiver habilitado, esses dispositivos terão acesso aos recursos internos.  

     - **Em não conformidade** – os dispositivos sem política de conformidade atribuída são considerados em não conformidade com a política. Se o acesso condicional estiver habilitado, esses dispositivos serão bloqueados dos recursos internos, de acordo com as condições na política de acesso condicional.  

4. Clique em Salvar.  

É altamente recomendável que você implante pelo menos uma política de conformidade para cada plataforma a todos os usuários em seu ambiente. Em seguida, defina essa configuração como **Em não conformidade** para garantir a segurança de seus recursos internos. Para obter mais informações, veja a postagem de blog [Aprimoramentos de Segurança no Serviço Intune](https://aka.ms/compliance_policies).



## <a name="next-steps"></a>Próximas etapas  
[Criar e implantar uma política de conformidade de dispositivo](/sccm/mdm/deploy-use/create-compliance-policy)

### <a name="see-also"></a>Consulte também  
 [Gerenciar o acesso aos serviços no Configuration Manager](/sccm/protect/deploy-use/manage-access-to-services)
