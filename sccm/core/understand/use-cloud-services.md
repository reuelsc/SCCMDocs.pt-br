---
title: "Usar serviços de nuvem com o Configuration Manager | Microsoft Docs"
description: Provisione recursos de nuvem para o System Center Configuration Manager complementar sua infraestrutura local.
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 24fca61e-9cdb-447a-ad7a-f4d2e4fd6704
caps.latest.revision: "10"
caps.handback.revision: "0"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 52f7c63d155d5c34f0f12e13020767dec1867dab
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/07/2017
---
# <a name="use-cloud-services-with-system-center-configuration-manager"></a>Usar serviços de nuvem com o System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

O System Center Configuration Manager dá suporte a várias opções baseadas em nuvem. Elas podem complementar sua infraestrutura local e podem ajudar a resolver problemas comerciais como:  

-   Como gerenciar BYOD (usando o Intune para o gerenciamento de dispositivos móveis).  

-   Como fornecer recursos de conteúdo a clientes isolados ou recursos na intranet, fora do firewall corporativo (usando pontos de distribuição baseados em nuvem).  

-   Como escalar horizontalmente a infraestrutura quando o hardware físico não estiver disponível ou não estiver posicionado de modo lógico para dar suporte às suas necessidades (usando máquinas virtuais do Microsoft Azure).  

Embora o provisionamento de recursos de nuvem não seja algo que você deva fazer antes de implantar o Configuration Manager, pode ser útil entender essas opções antes avançar muito em um plano de design de hierarquia. O uso de recursos de nuvem pode economizar dinheiro e tempo ao solucionar problemas comerciais que a infraestrutura local não consegue.  

## <a name="cloud-based-resources-you-can-use-with-configuration-manager"></a>Recursos baseados em nuvem que você pode usar com o Configuration Manager  
 Como cada opção tem diferentes requisitos, investigue-os em mais detalhes para compreender os pré-requisitos exclusivos, as limitações e os potenciais para custos adicionais com base no uso.  

-   Para obter mais informações sobre pontos de distribuição baseados em nuvem, consulte a seção [Install cloud-based distribution points (Instalar pontos de distribuição baseados em nuvem)](/sccm/core/servers/deploy/configure/install-cloud-based-distribution-points-in-microsoft-azure).

-   Para obter mais informações sobre o Azure, consulte [Azure](http://go.microsoft.com/fwlink/p/?LinkId=262965) na Biblioteca MSDN.  

### <a name="azure-virtual-machines-for-cloud-based-infrastructure"></a>Máquinas virtuais do Azure (para infraestrutura baseada em nuvem)  
 O Configuration Manager dá suporte ao uso de computadores executados em máquinas virtuais no Azure da mesma forma que quando são executados localmente em sua rede corporativa física. Você pode usar máquinas virtuais do Azure nos seguintes cenários:  

-   **Cenário 1:** é possível executar o Configuration Manager em uma máquina virtual e usá-lo para gerenciar clientes instalados em outras máquinas virtuais.  

-   **Cenário 2:** é possível executar o Configuration Manager em uma máquina virtual e usá-lo para gerenciar clientes que não estão sendo executados no Azure.  

-   **Cenário 3:** é possível executar diferentes funções do sistema de sites do Configuration Manager em máquinas virtuais durante a execução de outras funções em sua rede corporativa física (com conectividade de rede apropriada para comunicações).  

Os mesmos requisitos para redes, sistemas operacionais e hardware que se aplicam à instalação do Configuration Manager na sua rede corporativa física também se aplicam à instalação do Configuration Manager no Azure.  

É necessária uma assinatura do Azure para usar máquinas virtuais do Azure. Você incorre em encargos com base no número de máquinas virtuais usadas, sua configuração e uso de recursos baseados em nuvem.  

Além disso, os sites e os clientes do Configuration Manager executados em máquinas virtuais do Azure estão sujeitos aos mesmos requisitos de licença que as instalações locais.  

### <a name="azure-services-for-cloud-based-distribution-points"></a>Serviços do Azure (para pontos de distribuição baseados em nuvem)  
 É possível usar um serviço do Azure para hospedar um ponto de distribuição do Configuration Manager, chamado de ponto de distribuição baseado em nuvem. É possível [usar um ponto de distribuição baseado em nuvem com o System Center Configuration Manager](../../core/plan-design/hierarchy/use-a-cloud-based-distribution-point.md) em conjunto com pontos de distribuição locais e pontos de distribuição implantados em máquinas virtuais do Azure.  

 Isso é diferente de usar uma máquina virtual do Azure, em que você implanta uma função de sistema de sites. Pontos de distribuição baseados em nuvem:  

-   São executados como um serviço no Azure e não em uma máquina virtual.  

-   Dimensionam automaticamente para atender ao aumento nas solicitações de conteúdo de clientes.  

-   Dão suporte a clientes na Internet e intranet.  

É necessária uma assinatura do Azure para hospedar os pontos de distribuição. Você incorre em encargos com base na quantidade de dados transferidos de e para o serviço.  

### <a name="microsoft-intune-for-mobile-device-management"></a>Microsoft Intune (para gerenciamento de dispositivo móvel)  
 É possível integrar sua assinatura do Microsoft Intune ao Configuration Manager para habilitar o gerenciamento de dispositivos que usam o serviço do Intune. Essa integração:  

-   É chamada de configuração híbrida e estende o Configuration Manager (ou o Intune, dependendo da sua perspectiva) para dar suporte a uma grande variedade de dispositivos.  

-   Requer a função do sistema de sites do conector do Microsoft Intune.  

-   Requer que você tenha uma assinatura separada do Intune com licenças suficientes para os dispositivos que você gerenciará com o Intune.  

Embora o Intune use o Azure, ele não requer que você configure o Azure de modo independente e você não está sujeito a custos adicionais além da assinatura do Intune.  

### <a name="additional-configuration-manager-capabilities"></a>Recursos adicionais do Configuration Manager  
 Alguns recursos do Configuration Manager podem se conectar a serviços baseados em nuvem, como:  

-   WSUS (Windows Server Update Services).  

-   A nuvem de serviço do Configuration Manager para baixar atualizações do Configuration Manager.  

Esses recursos adicionais não exigem que você tenha uma assinatura do Azure. Você não precisa configurar conexões, certificados ou serviços específicos na nuvem. Em vez disso, eles são automaticamente gerenciados pelo Configuration Manager por você. Tudo o que você precisa fazer é garantir que os dispositivos e sistemas de sites aplicáveis tenham acesso às URLs com base na Internet.  

##  <a name="BKMK_CloudSec"></a> Segurança para serviços baseados em nuvem  
 O Configuration Manager usa certificados para provisionar e acessar seu conteúdo no Azure e para gerenciar os serviços que você usa. O Configuration Manager criptografa os dados armazenados no Azure, mas não introduz controles de segurança ou de dados adicionais além daqueles fornecidos pelo Azure.  

 Para obter mais informações, consulte os detalhes para os diferentes cenários de recursos baseados em nuvem. Você também pode exibir os seguintes tópicos para segurança do Azure:  

-   [Azure: noções básicas sobre o gerenciamento da conta de segurança no Azure](http://go.microsoft.com/fwlink/p/?LinkId=262968)  

-   [Visão geral da segurança do Azure](http://go.microsoft.com/fwlink/p/?LinkId=262970)  

-   [Get Past the Security Crossroads in Your Cloud Migration (Passar pelos cruzamentos de segurança em sua migração de nuvem)](http://go.microsoft.com/fwlink/p/?LinkId=262971)  

-   [Data Security in Azure Part 1 of 2 (Segurança de dados no Azure, parte 1 de 2)](http://go.microsoft.com/fwlink/p/?LinkId=262974)  
