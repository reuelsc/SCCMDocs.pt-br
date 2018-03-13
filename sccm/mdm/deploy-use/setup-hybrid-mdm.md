---
title: "Configurar MDM híbrido"
titleSuffix: Configuration Manager
description: "Configure o registro de dispositivo híbrido com o Configuration Manager e o Intune."
ms.custom: na
ms.date: 03/08/2018
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: bb95154b-f63e-4491-896e-41d732c802f8
caps.latest.revision: 
caps.handback.revision: 
author: dougeby
ms.author: dougeby
manager: angrobe
ms.openlocfilehash: 9c233a8601d68aae76b105ff86afe41d4121da40
ms.sourcegitcommit: b653342fb5d69a16e71b3548a7e9a2e47e54bf88
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/12/2018
---
# <a name="setup-hybrid-mobile-device-management-mdm-with-system-center-configuration-manager-and-microsoft-intune"></a>Configurar o MDM (gerenciamento de dispositivo móvel) híbrido com o System Center Configuration Manager e com o Microsoft Intune

*Aplica-se a: System Center Configuration Manager (Branch Atual)*


Antes de poder gerenciar dispositivos iOS, Windows e Android com o Configuration Manager, eles devem ser registrados com o Intune. Use as etapas a seguir para configurar o registro de dispositivo híbrido com o Configuration Manager usando o Intune. Ao concluir as etapas a seguir, você habilitará o registro de BYOD (“traga seu próprio dispositivo”) para seus usuários. Essas etapas também são pré-requisitos para [registrar dispositivos BYOD](enroll-hybrid-ios-mac.md) e [registrar dispositivos da empresa](enroll-company-owned-devices.md).

 |Etapas|Detalhes|  
 |-----------|-------------|  
 |**Etapa 1:** [criar uma coleção de MDM](create-mdm-collection.md)|Crie uma coleção de usuários do Configuration Manager com os usuários cujos dispositivos podem ser registrados|  
 |**Etapa 2:** [requisitos de nome de domínio](confirm-dns.md)|Confirme se o gerenciamento de usuários do Active Directory e o DNS (Serviço de Nomes de Domínio) da sua organização atendem aos requisitos de MDM|
 |**Etapa 3:** [configurar a assinatura do Intune](configure-intune-subscription.md)|O serviço Intune permite gerenciar dispositivos pela Internet.|  
 |**Etapa 4:** [adicionar termos e condições](terms-and-conditions.md)| Crie termos e condições com os quais os usuários devem concordar antes de poderem usar o aplicativo do Portal da Empresa|
 |**Etapa 5:** [criar um ponto de conexão de serviço](create-service-connection-point.md)|O ponto de conexão de serviço envia as configurações e informações da implantação de software para o Configuration Manager e recupera mensagens de status e inventário dos dispositivos móveis. |  
 |**Etapa 6:** [habilitar o registro de plataforma](enable-platform-enrollment.md)|O registro do MDM para dispositivos iOS e Windows exige etapas adicionais para a comunicação entre o serviço e os dispositivos. O Android não exige nenhuma configuração adicional.|  
 |**Etapa 7:** [configurar gerenciamento adicional](set-up-additional-management.md)|(Opcional) Configure o acesso condicional e itens de configuração para dispositivos registrados|
 |**Etapa 8:** [verificar a configuração do MDM](verify-mdm-configuration.md)|Veja os arquivos de log para confirmar que o ponto de conexão de serviço foi criado com êxito e as contas de usuário estão sincronizando.|

Procurando o Intune sem o Configuration Manager?
> [!div class="button"]
[Exibir documentos do Intune >](https://docs.microsoft.com/intune/deploy-use/enroll-devices-in-microsoft-intune)


## <a name="enroll-devices"></a>Registrar dispositivos
Após a conclusão da configuração híbrida, os dispositivos podem ser registrados no Configuration Manager de várias maneiras:
- **Dispositivos da empresa (COD):** [Registrar dispositivos da empresa](enroll-company-owned-devices.md) fornece orientação sobre diferentes formas específicas à plataforma para registrar dispositivos da empresa.
- **Dispositivos do usuário (BYOD):** [registrar dispositivos do usuário (BYOD)](enroll-hybrid-ios-mac.md) fornece orientação sobre como registrar dispositivos de propriedade do usuário.
