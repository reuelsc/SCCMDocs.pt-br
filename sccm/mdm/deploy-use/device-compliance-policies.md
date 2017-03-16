---
title: "Políticas de conformidade de dispositivo | Microsoft Docs"
description: "Saiba como gerenciar as políticas de conformidade no System Center Configuration Manager para tornar aos dispositivos compatíveis políticas de acesso condicional."
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ad8fa94d-45bb-4c94-8d86-31234c5cf21c
caps.latest.revision: 18
caps.handback.revision: 0
author: andredm7
ms.author: andredm
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 2c723fe7137a95df271c3612c88805efd8fb9a77
ms.openlocfilehash: ad9ea7b29e03bb514fe23fdf761b312c85c16714
ms.lasthandoff: 03/06/2017

---
# <a name="device-compliance-policies-in-system-center-configuration-manager"></a>Políticas de conformidade de dispositivo no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

As **políticas de conformidade** no System Center Configuration Manager definem as regras e configurações às quais um dispositivo deve obedecer para ser considerado compatível pelas políticas de acesso condicional. Você também pode usar as políticas de conformidade para monitorar e corrigir problemas com dispositivos, independentemente do acesso condicional.  


> [!IMPORTANT]  
>  Este artigo descreve as políticas de conformidade para dispositivos gerenciados pelo Microsoft Intune.    As políticas de conformidade para PCs gerenciados pelo System Center Configuration Manager são descritas em [Gerenciar o acesso aos serviços do O365 para PCs gerenciados pelo System Center Configuration Manager](../../protect/deploy-use/manage-access-to-o365-services-for-pcs-managed-by-sccm.md).  

 Essas regras incluem requisitos, como:  

-   PIN e senhas para acessar um dispositivo

-   Criptografia dos dados armazenados no dispositivo

-   Se o dispositivo está desbloqueado ou com raiz  

-   Se o email no dispositivo é gerenciado por uma política do Intune ou se o dispositivo é relatado como não íntegro pelo serviço de atestado de integridade de dispositivo do Windows.  


 Implante políticas de conformidade em coleções de usuários. Quando uma política de conformidade é implantada para um usuário, todos os dispositivos de usuários são verificados quanto à conformidade.  

 A tabela a seguir lista os tipos de dispositivos suportados pelas políticas de conformidade e como configurações não compatíveis são gerenciadas quando a política é usada com uma política de acesso condicional.  

|Regra|Windows 8.1 e posterior|Windows Phone 8.1 e posterior|iOS 6.0 e posterior|Android 4.0 e posterior ou Samsung KNOX Standard 4.0 e posterior|  
|----------|---------------------------|---------------------------------|-----------------------|---------------------------|-----------------------------------------|  
|**Configuração de senha ou PIN**|Corrigida|Corrigida|Corrigida|Em Quarentena|  
|**Criptografia de dispositivo**|N/D|Corrigida|Corrigida (pela definição do PIN)|Em Quarentena|  
|**Dispositivo com jailbreak ou root**|N/D|N/D|Em Quarentena (não é uma configuração)|Em Quarentena (não é uma configuração)|  
|**Perfil de email**|N/D|N/D|Em Quarentena|N/D|  
|**Versão mínima do SO**|Em Quarentena|Em Quarentena|Em Quarentena|Em Quarentena|  
|**Versão máxima do SO**|Em Quarentena|Em Quarentena|Em Quarentena|Em Quarentena|  
|**Atestado de Integridade do Dispositivo (atualização&1602;)**|A configuração não é aplicável ao Windows 8.1<br /><br /> O Windows 10 e o Windows 10 Mobile estão em quarentena.|N/D|N/D|N/D|  

 **Corrigida** = A conformidade é imposta pelo sistema operacional do dispositivo (por exemplo, o usuário será forçado a definir um PIN).  Nunca há um caso em que a configuração será fora de conformidade.  

 **Em Quarentena** = O sistema operacional do dispositivo não impõe conformidade (por exemplo, dispositivos Android não forçam o usuário a criptografar o dispositivo).  Nesse caso:  

-   O dispositivo será bloqueado se o usuário for afetado pela política de acesso condicional.  

-   O portal da empresa ou um portal da Web notificará o usuário sobre quaisquer problemas de conformidade.  


### <a name="next-steps"></a>Próximas etapas  
[Criar e implantar uma política de conformidade de dispositivo](create-compliance-policy.md)
### <a name="see-also"></a>Consulte também  
 [Gerenciar o acesso a serviços no System Center Configuration Manager](../../protect/deploy-use/manage-access-to-services.md)
