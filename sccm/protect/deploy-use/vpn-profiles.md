---
title: Perfis VPN no System Center Configuration Manager | Microsoft Docs
description: "Saiba como usar perfis de VPN no System Center Configuration Manager para implantar as configurações de VPN para usuários em sua organização."
ms.custom: na
ms.date: 11/27/2016
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
author: Nbigman
ms.author: nbigman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 593fbd0587d54490246f48ae54f666bac6b7830d
ms.openlocfilehash: 0ff83aed4d5e19806a8c69f4b45e39a6156dee7e


---
# <a name="vpn-profiles-in-system-center-configuration-manager"></a>Perfis VPN no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*


Use os perfis de VPN no System Center Configuration Manager (também conhecido como ConfigMgr ou SCCM) para implantar as configurações de VPN para usuários em sua organização. Ao implantar essas configurações, você minimiza o esforço do usuário final necessário para conectar-se aos recursos na rede da empresa.  

 Por exemplo, você deseja provisionar todos os dispositivos que executam o sistema operacional iOS com as configurações necessárias para se conectar ao compartilhamento de arquivos na rede corporativa. Você pode criar um perfil VPN que contém as configurações necessárias para conectar-se à rede corporativa e implantar esse perfil a todos os usuários que possuem dispositivos que executam o iOS na sua hierarquia. Os usuários de dispositivos iOS veem a conexão VPN na lista de redes disponíveis e podem se conectar a essa rede com o mínimo de esforço.  

 Quando você cria um perfil VPN, pode incluir uma grande variedade de configurações de segurança, inclusive certificados para validação de servidor e autenticação cliente que foram provisionados usando os perfis de certificado do System Center Configuration Manager. Para obter mais informações sobre perfis de certificado, consulte [Perfis de certificado do System Center Configuration Manager](introduction-to-certificate-profiles.md).  

 As seções a seguir explicam quais dispositivos você poderá configurar com perfis de VPN se usar o Configuration Manager ou o Configuration Manager com o Microsoft Intune.  

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

## <a name="vpn-profiles-when-using-configuration-manager-together-with-intune"></a>Perfis de VPN usando o Configuration Manager junto com o Intune  
 Para implantar perfis em dispositivos iOS, Android, Windows Phone e Windows 8.1, esses dispositivos devem ser registrados no Microsoft Intune. Dispositivos em outras plataformas também podem ser registrados no Intune. Para obter informações sobre como registrar, veja [Gerenciar dispositivos móveis com o Microsoft Intune](https://technet.microsoft.com/en-us/library/dn646962.aspx). Esta tabela mostra qual tipo de conexão tem suporte para cada plataforma de dispositivo:  

|Tipo de conexão|iOS e Mac OS X|Android|Windows 8.1|Windows RT|Windows RT 8.1|Windows Phone 8.1|Windows 10 Desktop e Mobile|  
|---------------------|----------------------|-------------|-----------------|----------------|--------------------|-----------------------|-----------------------------------|  
|Cisco AnyConnect|Sim|Sim|Não|Não|Não|Não|Sim (OMA-URI)|  
|Pulse Secure|Sim|Sim|Sim|Não|Sim|Sim|Sim|  
|F5 Edge Client|Sim|Sim|Sim|Não|Sim|Sim|Sim|  
|Dell SonicWALL Mobile Connect|Sim|Sim|Sim|Não|Sim|Sim|Sim|  
|Check Point Mobile VPN|Sim|Sim|Sim|Não|Sim|Sim|Sim|  
|Microsoft SSL (SSTP)|Não|Não|Sim|Sim|Sim|Não|Não|  
|Microsoft Automatic|Não|Não|Sim|Sim|Sim|Não|Sim (OMA-URI)|  
|IKEv2|Sim (Política personalizada)|Não|Sim|Sim|Sim|Sim|Sim (OMA-URI)|  
|PPTP|Sim|Não|Sim|Sim|Sim|Não|Sim (OMA-URI)|  
|L2TP|Sim|Não|Sim|Sim|Sim|Não|Sim (OMA-URI)|  

### <a name="next-steps"></a>Próximas etapas  
 Use os tópicos a seguir para ajudar a planejar, configurar, operar e manter perfis de VPN no Configuration Manager.  

-   [Pré-requisitos para perfis de VPN no System Center Configuration Manager](../plan-design/prerequisites-for-wifi-vpn-profiles.md)  

-   [Segurança e privacidade para perfis de VPN no System Center Configuration Manager](../plan-design/security-and-privacy-for-wifi-vpn-profiles.md)



<!--HONumber=Dec16_HO3-->


