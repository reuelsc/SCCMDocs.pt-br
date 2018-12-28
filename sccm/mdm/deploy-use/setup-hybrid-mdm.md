---
title: Configurar o MDM híbrido
titleSuffix: Configuration Manager
description: Configure o registro de dispositivo híbrido com o Configuration Manager e o Intune.
ms.date: 08/14/2018
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: bb95154b-f63e-4491-896e-41d732c802f8
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: a69f849d4843ff7a0cf7df4a0b6de044a9506301
ms.sourcegitcommit: 48098f9fb2f447672bf36d50c9f58a3d26acb9ed
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2018
ms.locfileid: "53421800"
---
# <a name="set-up-hybrid-mdm-with-configuration-manager-and-microsoft-intune"></a>Configure o MDM híbrido com o Configuration Manager e o Microsoft Intune

*Aplica-se a: System Center Configuration Manager (Branch atual)*


Antes de poder gerenciar dispositivos iOS, Windows e Android com o Configuration Manager, eles devem ser registrados com o Intune. Use as etapas a seguir para configurar o registro de dispositivo híbrido com o Configuration Manager usando o Intune. Ao concluir as etapas a seguir, você habilitará o registro de BYOD ("traga seu próprio dispositivo") para seus usuários. Essas etapas também são pré-requisitos para [registrar dispositivos BYOD](enroll-hybrid-ios-mac.md) e [registrar dispositivos da empresa](enroll-company-owned-devices.md).

> [!Important]  
> O gerenciamento híbrido de dispositivos móveis é um [recurso preterido](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures) desde 14 de agosto de 2018. Para saber mais, confira [O que é o MDM híbrido](/sccm/mdm/understand/hybrid-mobile-device-management).<!--Intune feature 2683117-->  



## <a name="set-up-steps"></a>Etapas de configuração

 |Etapas|Detalhes|  
 |-----------|-------------|  
 |**Etapa 1:** [Criar uma coleção de MDM](create-mdm-collection.md)|Crie uma coleção de usuários do Configuration Manager com os usuários cujos dispositivos podem ser registrados|  
 |**Etapa 2:** [Requisitos de nome de domínio](confirm-dns.md)|Confirme se o gerenciamento de usuários do Active Directory e o DNS (Serviço de Nomes de Domínio) da sua organização atendem aos requisitos de MDM|
 |**Etapa 3:** [Configurar a assinatura do Intune](configure-intune-subscription.md)|O serviço Intune permite gerenciar dispositivos pela Internet.|  
 |**Etapa 4:** [Adicionar termos e condições](terms-and-conditions.md)| Crie termos e condições com os quais os usuários devem concordar antes de poderem usar o aplicativo do Portal da Empresa|
 |**Etapa 5:** [Criar um ponto de conexão de serviço](create-service-connection-point.md)|O ponto de conexão de serviço envia as configurações e informações da implantação de software para o Configuration Manager e recupera mensagens de status e inventário dos dispositivos móveis. |  
 |**Etapa 6:** [Habilitar o registro de plataforma](enable-platform-enrollment.md)|O registro do MDM para dispositivos iOS e Windows exige etapas adicionais para a comunicação entre o serviço e os dispositivos. O Android não exige nenhuma configuração adicional.|  
 |**Etapa 7:** [Configurar gerenciamento adicional](set-up-additional-management.md)|(Opcional) Configure o acesso condicional e itens de configuração para dispositivos registrados|
 |**Etapa 8:** [Verificar a configuração do MDM](verify-mdm-configuration.md)|Veja os arquivos de log para confirmar que o ponto de conexão de serviço foi criado com êxito e as contas de usuário estão sincronizando.|



## <a name="enroll-devices"></a>Registrar dispositivos

Após a conclusão da configuração híbrida, os dispositivos podem ser registrados no Configuration Manager de várias maneiras:

- **Dispositivos (COD) da empresa:** [Registrar dispositivos da empresa](enroll-company-owned-devices.md) fornece orientação sobre diferentes formas específicas da plataforma para registrar dispositivos da empresa  

- **Usuário – dispositivos (BYOD):** [Registrar dispositivos (BYOD) usuário](enroll-hybrid-ios-mac.md) fornece orientação sobre como registrar dispositivos do usuário  



## <a name="see-also"></a>Consulte também

Procurando o Intune sem o Configuration Manager?
> [!div class="button"]
> [Exibir documentos do Intune >](https://docs.microsoft.com/intune/deploy-use/enroll-devices-in-microsoft-intune)


