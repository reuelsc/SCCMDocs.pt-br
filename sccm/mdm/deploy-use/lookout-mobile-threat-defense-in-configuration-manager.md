---
title: Restringir o acesso com base em riscos
titleSuffix: Configuration Manager
description: Restrinja o acesso aos recursos da empresa com base em risco de dispositivo, rede e aplicativo.
ms.date: 08/14/2018
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 9083c571-f4fc-4a78-adc5-8aec84dabcbd
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 50d79da3ab4e7ace9a682baaa5cfd8d2bdbdce10
ms.sourcegitcommit: f9654cd1a3af6d67de52fedaccceb2e22dafc159
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/09/2019
ms.locfileid: "67678868"
---
# <a name="manage-access-to-company-resource-based-on-device-network-and-application-risk"></a>Gerenciar o acesso aos recursos da empresa com base em risco de dispositivo, rede e aplicativo

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Controle o acesso de dispositivos móveis a recursos corporativos com base na avaliação de riscos realizada pelo Lookout. O Lookout é uma solução de proteção contra ameaças ao dispositivo integrada ao Microsoft Intune. O risco é baseado em dados coletados pelo serviço do Lookout. Ele reúne dados de dispositivos referentes a vulnerabilidades do sistema operacional, aplicativos maliciosos instalados e perfis de rede mal-intencionados. 

Com base na avaliação de riscos relatada pelo Lookout, ativada por meio das políticas de conformidade do Configuration Manager, é possível configurar políticas de acesso condicional. Essas políticas permitem ou bloqueiam dispositivos que o Configuration Manager determina como não compatíveis devido a ameaças detectadas nesses dispositivos.

> [!Important]  
> O gerenciamento híbrido de dispositivos móveis é um [recurso preterido](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures) desde 14 de agosto de 2018. Para saber mais, confira [O que é o MDM híbrido](/sccm/mdm/understand/hybrid-mobile-device-management).<!--Intune feature 2683117-->  



## <a name="how-does-it-work"></a>Como isso funciona?

Como a implantação de MDM híbrida e a proteção contra ameaças ao dispositivo do Lookout ajudam a proteger os recursos da empresa?

O aplicativo móvel do Lookout (Lookout for Work) é executado em dispositivos móveis. Ele captura o sistema de arquivos, a pilha de rede e os dados de uso de dispositivos e aplicativos, quando disponíveis. O aplicativo envia esses dados para o serviço de nuvem de proteção contra ameaças ao dispositivo do Lookout para calcular um risco agregado do dispositivo quanto a ameaças móveis. Use o console do Lookout para alterar a classificação do nível de risco das ameaças de acordo com suas necessidades.  

A política de conformidade do Configuration Manager agora inclui uma nova regra do Lookout Mobile Threat Protection, que se baseia na avaliação de risco de ameaças ao dispositivo do Lookout. Ao habilitar essa regra, o Configuration Manager avalia o dispositivo quanto à conformidade.

Se o dispositivo não estiver em conformidade com a política, você pode bloquear o acesso a recursos como Exchange Online e SharePoint Online usando políticas de acesso condicional. Quando o acesso é bloqueado, o usuário final recebe um passo a passo para ajudar a resolver o problema e obter acesso aos recursos da empresa. O usuário inicia este passo a passo pelo aplicativo Lookout for Work.



## <a name="supported-platforms"></a>Plataformas com Suporte

- **Android 4.1 e posterior**, registrado no Microsoft Intune.  

- **iOS 8 e posterior**, registrado no Microsoft Intune.  


Para saber mais sobre plataformas e idiomas compatíveis com o Lookout, consulte este [artigo de suporte do Lookout](https://personal.support.lookout.com/hc/articles/114094140253).



## <a name="prerequisites"></a>Pré-requisitos

- [MDM híbrido](/sccm/mdm/understand/hybrid-mobile-device-management)  

- Uma assinatura do Microsoft Intune e o Azure Active Directory.  

- Uma assinatura empresarial do Lookout Mobile Endpoint Security. Para saber mais, confira [Lookout Mobile Endpoint Security](https://www.lookout.com/products/mobile-endpoint-security).  



## <a name="example-scenarios"></a>Cenários de exemplo


### <a name="control-access-based-on-threat-from-malicious-apps"></a>Controlar o acesso com base em ameaças de aplicativos mal-intencionados

Quando aplicativos mal-intencionados, como malware, são detectados no dispositivo, é possível impedir que esses dispositivos:

- Conectem-se ao email corporativo antes de resolver a ameaça  

- Sincronizem arquivos corporativos usando o aplicativo OneDrive for Work  

- Acessem aplicativos essenciais para os negócios  

#### <a name="access-blocked-when-malicious-apps-are-detected"></a>Acesso bloqueado ao detectar aplicativos maliciosos

![Política de acesso condicional que bloqueia o acesso ao detectar um aplicativo malicioso](media/config-mgr-maliciousapps_blocked.png)

#### <a name="device-unblocked-and-is-able-to-access-company-resources-when-the-threat-is-remediated"></a>Dispositivo desbloqueado e capaz de acessar os recursos da empresa quando a ameaça é remediada

![Política de acesso condicional concedendo o acesso quando o dispositivo está em conformidade](media/config-mgr-maliciousapps-unblocked.png)


### <a name="control-access-based-on-threat-to-network"></a>Controlar o acesso com base em ameaças à rede

Detecte as ameaças à sua rede, como ataques de interceptação, e restrinja o acesso às redes Wi-Fi com base no risco ao dispositivo.

#### <a name="access-to-network-through-wifi-blocked"></a>Acesso à rede através de Wi-Fi bloqueado

![Acesso condicional bloqueando o acesso a Wi-Fi com base em ameaças à rede](media/config-mgr-network-wifi-blocked.png)

#### <a name="access-granted-on-remediation"></a>Acesso concedido após correção

![Acesso condicional permitindo o acesso após a correção da ameaça](media/config-mgr-network-wifi-unblocked.png)


### <a name="control-access-to-sharepoint-online-based-on-threat-to-network"></a>Controlar o acesso ao SharePoint Online com base em ameaças à rede

Detecte ameaças à sua rede, como ataques de interceptação, e evite a sincronização de arquivos corporativos com base no risco ao dispositivo.

#### <a name="access-blocked-sharepoint-online-based-on-network-threat-detected-on-the-device"></a>Acesso bloqueado ao SharePoint Online com base em ameaça à rede detectada no dispositivo

![Acesso condicional bloqueando o acesso do dispositivo ao SharePoint Online](media/config-mgr-network-spo-blocked.png)


#### <a name="access-granted-on-remediation"></a>Acesso concedido após correção

![Acesso condicional permitindo o acesso após a correção da ameaça](media/config-mgr-network-spo-unblocked.png)



## <a name="next-steps"></a>Próximas etapas

Para implementar essa solução, siga estas etapas:  

1. [Configurar sua assinatura do Lookout Mobile Threat Protection](set-up-your-subscription-with-lookout.md)
2. [Habilitar a conexão do Lookout MTP no Intune](enable-lookout-connection-in-intune.md)
3.  [Configurar e implantar o aplicativo Lookout for Work](configure-and-deploy-lookout-for-work-apps.md)
4. [Configurar a política de conformidade](enable-device-threat-protection-rule-compliance-policy.md)
5. [Solucionar problemas de integração do Lookout](troubleshoot-lookout-integration.md)
