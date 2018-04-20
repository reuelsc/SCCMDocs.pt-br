---
title: Perfis de VPN
titleSuffix: Configuration Manager
description: Saiba como usar perfis de VPN no System Center Configuration Manager para implantar as configurações de VPN para usuários em sua organização.
ms.custom: na
ms.date: 04/10/2018
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c0f094f1-852e-4606-91db-97846d8f0772
caps.latest.revision: 6
caps.handback.revision: 0
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: d30e7cc834f1693f2cbcf2db840d650421062a19
ms.sourcegitcommit: fb84bcb31d825f454785e3d9d8be669e00fe2b27
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="vpn-profiles-in-system-center-configuration-manager"></a>Perfis VPN no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

<!--1283610-->
Para implantar as configurações de VPN para os usuários da organização, use perfis de VPN no Configuration Manager. Ao implantar essas configurações, você minimiza o esforço do usuário final necessário para conectar-se aos recursos na rede da empresa.  

 Por exemplo, você deseja definir todos os dispositivos Windows 10 com as configurações necessárias para conectar-se a um compartilhamento de arquivos na rede corporativa. Você pode criar um perfil de VPN com as configurações necessárias para conectar-se à rede corporativa. Em seguida, implantar esse perfil para todos os usuários que têm dispositivos que executam o Windows 10. Esses usuários verão a conexão de VPN na lista de redes disponíveis e poderão se conectar facilmente.  

 Ao criar um perfil VPN, você pode incluir uma várias configurações de segurança. Essas configurações incluem os certificados para validação do servidor e autenticação do cliente que você provisionou com os perfis de certificado do Configuration Manager. Para obter mais informações, consulte [Certificate profiles (Perfis de Certificado)](introduction-to-certificate-profiles.md).  

> [!Note]  
> O Configuration Manager não habilita esse recurso opcional por padrão. Você precisa habilitar esse recurso antes de usá-lo. Para obter mais informações, confira [Habilitar recursos opcionais de atualizações](/sccm/core/servers/manage/install-in-console-updates#bkmk_options).<!--505213-->  


 Confira [Perfis de VPN em dispositivos móveis](/sccm/mdm/deploy-use/create-vpn-profiles) para examinar os dispositivos que você pode configurar durante o uso do Configuration Manager com o Microsoft Intune.  

## <a name="vpn-profiles-when-using-configuration-manager"></a>Perfis de VPN usando o Configuration Manager  
 A tabela a seguir descreve os perfis de VPN que você pode configurar para várias plataformas de dispositivo.  

|Tipo de conexão|Windows 8.1|Windows RT|Windows RT 8.1|Windows 10|  
|---------------------|-----------------|----------------|--------------------|----------------|  
|**Cisco AnyConnect**|Não|Não|Não|Não|  
|**Pulse Secure**|Sim|Não|Sim|Sim|  
|**F5 Edge Client**|Sim|Não|Sim|Sim|  
|**Dell SonicWALL Mobile Connect**|Sim|Não|Sim|Sim|  
|**Check Point Mobile VPN**|Sim|Não|Sim|Sim|  
|**Microsoft SSL (SSTP)**|Sim|Sim|Sim|Não|  
|**Microsoft Automatic**|Sim|Sim|Sim|Não|  
|**IKEv2**|Sim|Sim|Sim|Não|  
|**PPTP**|Sim|Sim|Sim|Não|  
|**L2TP**|Sim|Sim|Sim|Não|  

### <a name="next-steps"></a>Próximas etapas  
 Use os tópicos a seguir para ajudar a planejar, configurar, operar e manter perfis de VPN no Configuration Manager.  

-   [Pré-requisitos para perfis de VPN no System Center Configuration Manager](../plan-design/prerequisites-for-wifi-vpn-profiles.md)  

-   [Segurança e privacidade para perfis de VPN no System Center Configuration Manager](../plan-design/security-and-privacy-for-wifi-vpn-profiles.md)
