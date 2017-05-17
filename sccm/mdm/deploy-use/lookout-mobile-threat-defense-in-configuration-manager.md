---
title: Restringir o acesso com base no risco | Microsoft Docs
description: Restrinja o acesso aos recursos da empresa com base em risco de dispositivo, rede e aplicativo.
ms.custom: na
ms.date: 04/25/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 9083c571-f4fc-4a78-adc5-8aec84dabcbd
caps.latest.revision: 
author: andredm7
ms.author: andredm
manager: angrobe
ms.translationtype: Human Translation
ms.sourcegitcommit: c6a6137fa978e1ea28aefea2aea4e29ba661efd6
ms.openlocfilehash: 21841d97387f07f53993d957641f9ad892d723c2
ms.contentlocale: pt-br
ms.lasthandoff: 05/17/2017


---
# <a name="manage-access-to-company-resource-based-on-device-network-and-application-risk"></a>Gerenciar o acesso aos recursos da empresa com base em risco de dispositivo, rede e aplicativo

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

É possível controlar o acesso de dispositivos móveis aos recursos corporativos, com base na avaliação de risco realizada pelo Lookout, uma solução de proteção contra ameaças ao dispositivo integrada ao Microsoft Intune. O risco se baseia na telemetria que o serviço Lookout coleta dos dispositivos em relação às vulnerabilidades do sistema operacional, aos aplicativos mal-intencionados instalados e aos perfis de rede mal-intencionados. 

Com base na avaliação de risco relatada do Lookout, habilitada por meio das políticas de conformidade do SCCM (System Center Configuration Manager), é possível configurar políticas de acesso condicional e permitir ou bloquear dispositivos se for determinado que eles não estão em conformidade, devido a ameaças detectadas nesses dispositivos.

A [implantação de MDM híbrida (SCCM com o Intune)](https://docs.microsoft.com/sccm/mdm/understand/choose-between-standalone-intune-and-hybrid-mobile-device-management) oferece a você a capacidade de controlar o acesso aos recursos e dados da empresa com base na avaliação de risco fornecida por soluções de proteção contra ameaças ao dispositivo como o Lookout.

## <a name="how-do-the-hybrid-mdm-deployment-and-lookout-device-threat-protection-help-protect-company-resources"></a>Como a implantação de MDM híbrida e a proteção contra ameaças ao dispositivo do Lookout ajudam a proteger os recursos da empresa?
O aplicativo móvel do Lookout (Lookout for Work), executado em dispositivos móveis, captura o sistema de arquivos, a pilha de rede, a telemetria de dispositivos e aplicativos (quando disponível) e envia todos eles para o serviço de nuvem de proteção contra ameaças ao dispositivo do Lookout, a fim de calcular um risco ao dispositivo agregado de ameaças móveis. Também é possível alterar a classificação do nível de risco das ameaças no console do Lookout, de acordo com suas necessidades.  

A política de conformidade do SCCM agora inclui uma nova regra do Lookout Mobile Threat Protection, que se baseia na avaliação de risco de ameaças ao dispositivo do Lookout. Quando essa regra é habilitada, a conformidade do dispositivo é avaliada.

Se for determinado que o dispositivo não está em conformidade com a política de conformidade, o acesso a recursos como Exchange Online e SharePoint Online poderá ser bloqueado usando políticas de acesso condicional. Quando o acesso é bloqueado, os usuários finais recebem um passo a passo para ajudar a resolver o problema e obter acesso aos recursos da empresa. Esse passo a passo é iniciado por meio do aplicativo Lookout for Work.

## <a name="supported-platforms"></a>Plataformas com suporte:
* **Android 4.1 e posterior**, registrado no Microsoft Intune.
* **iOS 8 e posterior**, registrado no Microsoft Intune.
Para obter informações sobre as plataformas e os idiomas com suporte no Lookout, consulte este [artigo](https://personal.support.lookout.com/hc/en-us/articles/114094140253).

## <a name="prerequisites"></a>Pré-requisitos:
* [Implantação de MDM híbrida](https://docs.microsoft.com/sccm/mdm/understand/choose-between-standalone-intune-and-hybrid-mobile-device-management)
* Uma assinatura do Microsoft Intune e o Azure Active Directory.
* Uma assinatura empresarial do Lookout Mobile EndPoint Security.  Para obter mais informações, consulte [Lookout Mobile Endpoint Security](https://www.lookout.com/products/mobile-endpoint-security)

## <a name="example-scenarios"></a>Cenários de exemplo
Estes são alguns cenários comuns:
### <a name="control-access-based-on-threat-from-malicious-apps"></a>Controlar o acesso com base em ameaças de aplicativos mal-intencionados:
Quando aplicativos mal-intencionados, como malware, são detectados no dispositivo, é possível impedir que esses dispositivos:
* Conectem-se ao email corporativo antes de resolver a ameaça.
* Sincronizem arquivos corporativos usando o aplicativo OneDrive for Work.
* Acessem aplicativos críticos para os negócios.

**Bloqueio do acesso quando aplicativos mal-intencionados forem detectados:**

![Diagrama que mostra a política de acesso condicional bloqueando o acesso quando for determinado que o dispositivo não está em conformidade, devido a aplicativos mal-intencionados no dispositivo](media/config-mgr-maliciousapps_blocked.png)

**Desbloqueio do dispositivo e permissão para acessar os recursos da empresa quando a ameaça é corrigida:**

![diagrama que mostra a política de acesso condicional concedendo o acesso quando for determinado que o dispositivo está em conformidade após a correção](media/config-mgr-maliciousapps-unblocked.png)
### <a name="control-access-based-on-threat-to-network"></a>Controlar o acesso com base em ameaças à rede:
Detecte as ameaças à sua rede, como ataques “man-in-the-middle”, e restrinja o acesso às redes WiFi com base no risco ao dispositivo.

**Bloqueio do acesso à rede por meio de WiFi:**

![Diagrama que mostra o acesso condicional bloqueando o acesso a WiFi com base em ameaças à rede](media/config-mgr-network-wifi-blocked.png)

**Concessão do acesso após a correção:**

![Diagrama que mostra o acesso condicional permitindo o acesso após a correção da ameaça](media/config-mgr-network-wifi-unblocked.png)
### <a name="control-access-to-sharepoint-online-based-on-threat-to-network"></a>Controlar o acesso ao SharePoint Online com base em ameaças à rede:

Detecte ameaças à sua rede, como ataques “man-in-the-middle”, e previna a sincronização de arquivos corporativos com base no risco ao dispositivo.

**Bloqueio do acesso ao SharePoint Online com base em ameaças à rede detectadas no dispositivo:**

![Diagrama mostrando o acesso condicional, bloqueando o acesso de dispositivo no SharePoint Online com base na detecção de ameaças](media/config-mgr-network-spo-blocked.png)


**Concessão do acesso após a correção:**

![Diagrama que mostra o acesso condicional permitindo o acesso após a correção da ameaça à rede](media/config-mgr-network-spo-unblocked.png)

## <a name="next-steps"></a>Próximas etapas
Estas são as principais etapas que devem ser seguidas para implementar essa solução:
1.    [Configurar sua assinatura do Lookout Mobile Threat Protection](set-up-your-subscription-with-lookout.md)
2.    [Habilitar a conexão do Lookout MTP no Intune](enable-lookout-connection-in-intune.md)
3.  [Configurar e implantar o aplicativo Lookout for Work](configure-and-deploy-lookout-for-work-apps.md)
4.    [Configurar a política de conformidade](enable-device-threat-protection-rule-compliance-policy.md)
5.    [Solucionar problemas de integração do Lookout](troubleshoot-lookout-integration.md)

