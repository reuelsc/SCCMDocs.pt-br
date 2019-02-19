---
title: Perguntas frequentes sobre o CMG
description: Use este artigo para responder a perguntas frequentes sobre o gateway de gerenciamento de nuvem
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 09/10/2018
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.assetid: 4c1a128d-22fb-49f1-8e0b-36513a8dc117
ms.collection: M365-identity-device-management
ms.openlocfilehash: bcc535c007fc081d2597e5c6dafc159ed1176f39
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56156865"
---
# <a name="frequently-asked-questions-about-the-cloud-management-gateway"></a>Perguntas frequentes sobre o gateway de gerenciamento de nuvem

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Este artigo responde às perguntas frequentes sobre o gateway de gerenciamento de nuvem. Para obter mais informações, consulte [Planejar o gateway de gerenciamento de nuvem](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway).


## <a name="frequently-asked-questions"></a>Perguntas frequentes

### <a name="what-certificates-do-i-need"></a>Quais certificados são necessários?

Para obter informações mais detalhadas, consulte [Certificados do gateway de gerenciamento de nuvem](/sccm/core/clients/manage/cmg/certificates-for-cloud-management-gateway).


### <a name="do-i-need-azure-expressroute"></a>O Azure ExpressRoute é necessário?

O [Azure ExpressRoute](/azure/expressroute/expressroute-introduction) possibilita que você estenda a rede local para a nuvem da Microsoft. O ExpressRoute, ou outras conexões de rede virtual desse tipo, não é necessário para o Gateway de Gerenciamento de Nuvem do Configuration Manager. O design do gateway de gerenciamento de nuvem permite que os clientes baseados na Internet se comuniquem por meio do serviço do Azure com os sistemas de sites locais sem nenhuma configuração de rede adicional. Para obter mais informações, consulte [Planejar o gateway de gerenciamento de nuvem](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway)

Caso sua organização use o ExpressRoute, uma melhor prática de segurança é isolar a assinatura do Azure para o gateway de gerenciamento de nuvem. Essa configuração garante que o serviço de Gateway de Gerenciamento de Nuvem não seja conectado acidentalmente dessa maneira. Para obter mais informações, consulte [Segurança e privacidade do gateway de gerenciamento de nuvem](/sccm/core/clients/manage/cmg/security-and-privacy-for-cloud-management-gateway).


### <a name="do-i-need-to-maintain-the-azure-virtual-machines"></a>É necessário manter as máquinas virtuais do Azure?

Nenhuma manutenção é necessária. O design do gateway de gerenciamento de nuvem usa o PaaS (plataforma como serviço) do Azure. Usando a assinatura fornecida, o Configuration Manager cria as VMs (máquinas virtuais), o armazenamento e a rede necessários. O Azure protege e atualiza a máquina virtual. Essas VMs não fazem parte do ambiente local, como é o caso do IaaS (infraestrutura como serviço). O gateway de gerenciamento de nuvem é um PaaS que estende o ambiente do Configuration Manager para a nuvem. 


### <a name="im-already-using-ibcm-if-i-add-cmg-how-do-clients-behave"></a>Já estou usando o IBCM. Se eu adicionar o CMG, como os clientes se comportarão?

Se você já implantou o [IBCM](/sccm/core/clients/manage/plan-internet-based-client-management) (gerenciamento de clientes baseado na Internet), implante também o gateway de gerenciamento de nuvem. Os clientes recebem a política para ambos os serviços. Conforme eles usam um perfil móvel na Internet, eles aleatoriamente selecionam e usam um desses serviços baseados na Internet.


### <a name="do-the-user-accounts-have-to-be-in-the-same-azure-subscription-as-the-subscription-that-hosts-the-cmg-cloud-service"></a>As contas de usuário precisam estar na mesma assinatura que a assinatura do Azure que hospeda o serviço de nuvem CMG?
<!--SCCMDocs-pr issue #2873--> Se o ambiente tiver mais de uma assinatura, você poderá implantar o CMG em qualquer assinaturas que possa hospedar serviços de nuvem do Azure. 

Essa pergunta é comum nos seguintes cenários:  

- Quando você tem ambientes do Azure AD e do Active Directory de teste e produção distintos, mas uma única assinatura de hospedagem do Azure centralizada  

- Seu uso do Azure cresceu organicamente entre diferentes equipes  

Quando você estiver usando uma implantação do Resource Manager, integre o locatário associado do Azure AD. Essa conexão permite que o Configuration Manager autentique-se no Azure para criar, implantar e gerenciar o CMG.  

Se você está usando a autenticação do Azure AD para os usuários e dispositivos gerenciados sobre o CMG, integre esse locatário do Azure AD. Para obter mais informações sobre os serviços do Azure para gerenciamento de nuvem, veja [Configurar serviços do Azure](/sccm/core/servers/deploy/configure/azure-services-wizard). Ao integrar cada locatário do Azure AD, um único CMG pode fornecer a autenticação do Azure AD para vários locatários, não importa o local de hospedagem.



## <a name="next-steps"></a>Próximas etapas

- [Plano para o gateway de gerenciamento de nuvem](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway)
- [Configurar o gateway de gerenciamento de nuvem](/sccm/core/clients/manage/cmg/setup-cloud-management-gateway)
- [Certificados para o gateway de gerenciamento de nuvem](/sccm/core/clients/manage/cmg/certificates-for-cloud-management-gateway)
- [Segurança e privacidade para o gateway de gerenciamento de nuvem](/sccm/core/clients/manage/cmg/security-and-privacy-for-cloud-management-gateway)
- [Tamanho e números de escala do gateway de gerenciamento de nuvem](/sccm/core/plan-design/configs/size-and-scale-numbers#bkmk_cmg)
