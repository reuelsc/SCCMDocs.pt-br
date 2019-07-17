---
title: Perguntas frequentes sobre o CMG
description: Use este artigo para responder a perguntas frequentes sobre o gateway de gerenciamento de nuvem
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 07/05/2019
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.assetid: 4c1a128d-22fb-49f1-8e0b-36513a8dc117
ms.collection: M365-identity-device-management
ms.openlocfilehash: 61afe2a98fa6ec76a872501d76293ab077cc2df8
ms.sourcegitcommit: 5e43c0c6b0b1f449e596f59ceaa92a9b6ca194cc
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/05/2019
ms.locfileid: "67572747"
---
# <a name="frequently-asked-questions-about-the-cloud-management-gateway"></a>Perguntas frequentes sobre o gateway de gerenciamento de nuvem

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Este artigo responde às perguntas frequentes sobre o gateway de gerenciamento de nuvem. Para obter mais informações, consulte [Planejar o gateway de gerenciamento de nuvem](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway).


## <a name="frequently-asked-questions"></a>Perguntas frequentes

### <a name="what-certificates-do-i-need"></a>Quais certificados são necessários?

Para obter informações mais detalhadas, consulte [Certificados do gateway de gerenciamento de nuvem](/sccm/core/clients/manage/cmg/certificates-for-cloud-management-gateway).


### <a name="do-i-need-azure-expressroute"></a>O Azure ExpressRoute é necessário?

Não. O [Azure ExpressRoute](/azure/expressroute/expressroute-introduction) possibilita que você estenda a rede local para a nuvem da Microsoft. O ExpressRoute, ou outras conexões de rede virtual desse tipo, não é necessário para o Gateway de Gerenciamento de Nuvem do Configuration Manager. O design do gateway de gerenciamento de nuvem permite que os clientes baseados na Internet se comuniquem por meio do serviço do Azure com os sistemas de sites locais sem nenhuma configuração de rede adicional. Para obter mais informações, consulte [Planejar o gateway de gerenciamento de nuvem](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway)

<!-- SCCMDocs#1659 -->

### <a name="do-i-need-to-maintain-the-azure-virtual-machines"></a>É necessário manter as máquinas virtuais do Azure?

Nenhuma manutenção é necessária. O design do gateway de gerenciamento de nuvem usa o PaaS (plataforma como serviço) do Azure. Usando a assinatura fornecida, o Configuration Manager cria as VMs (máquinas virtuais), o armazenamento e a rede necessários. O Azure protege e atualiza a máquina virtual. Essas VMs não fazem parte do ambiente local, como é o caso do IaaS (infraestrutura como serviço). O gateway de gerenciamento de nuvem é um PaaS que estende o ambiente do Configuration Manager para a nuvem. Para saber mais, confira [Protegendo Implantações de PaaS](/azure/security/security-paas-deployments).


### <a name="how-can-i-ensure-service-continuity-during-service-updates"></a>Como posso garantir a continuidade do serviço durante as atualizações do serviço?

Ao dimensionar o CMG para incluir duas ou mais instâncias, você se beneficia automaticamente de domínios de atualização no Microsoft Azure. Confira [Como atualizar um serviço de nuvem](/azure/cloud-services/cloud-services-update-azure-service).


### <a name="im-already-using-ibcm-if-i-add-cmg-how-do-clients-behave"></a>Já estou usando o IBCM. Se eu adicionar o CMG, como os clientes se comportarão?

Se você já implantou o [IBCM](/sccm/core/clients/manage/plan-internet-based-client-management) (gerenciamento de clientes baseado na Internet), implante também o gateway de gerenciamento de nuvem. Os clientes recebem a política para ambos os serviços. Conforme eles usam um perfil móvel na Internet, eles aleatoriamente selecionam e usam um desses serviços baseados na Internet.


### <a name="do-the-user-accounts-have-to-be-in-the-same-azure-subscription-as-the-subscription-that-hosts-the-cmg-cloud-service"></a>As contas de usuário precisam estar na mesma assinatura que a assinatura do Azure que hospeda o serviço de nuvem CMG?
<!--SCCMDocs-pr issue #2873-->
Se o ambiente tiver mais de uma assinatura, você pode implantar o CMG em qualquer assinaturas que possa hospedar serviços de nuvem do Azure. 

Essa pergunta é comum nos seguintes cenários:  

- Quando você tem ambientes do Azure AD e do Active Directory de teste e produção distintos, mas uma única assinatura de hospedagem do Azure centralizada  

- Seu uso do Azure cresceu organicamente entre diferentes equipes  

Quando você estiver usando uma implantação do Resource Manager, integre o locatário associado do Azure AD. Essa conexão permite que o Configuration Manager autentique-se no Azure para criar, implantar e gerenciar o CMG.  

Se você está usando a autenticação do Azure AD para os usuários e dispositivos gerenciados sobre o CMG, integre esse locatário do Azure AD. Para obter mais informações sobre os serviços do Azure para gerenciamento de nuvem, veja [Configurar serviços do Azure](/sccm/core/servers/deploy/configure/azure-services-wizard). Ao integrar cada locatário do Azure AD, um único CMG pode fornecer a autenticação do Azure AD para vários locatários, não importa o local de hospedagem.

### <a name="how-does-cmg-affect-my-clients-connected-via-vpn"></a>Como o CMG afeta meus clientes conectados por meio de VPN?

Normalmente, os clientes em roaming que se conectam ao seu ambiente por meio de uma VPN são detectados como voltados para a intranet. Eles tentam se conectar à sua infraestrutura local, como pontos de gerenciamento e pontos de distribuição. Alguns preferem ter os clientes em roaming gerenciados por serviços de nuvem, mesmo quando conectados por meio de VPN. Começando com a versão 1902, associa-se o CMG com um grupo de limites. Essa ação força esses clientes a não usar os sistemas de site locais. Para obter mais informações, consulte [Configurar grupos de limites](/sccm/core/clients/manage/cmg/setup-cloud-management-gateway#configure-boundary-groups).

### <a name="if-i-enable-a-cmg-will-my-clients-only-connect-to-the-cmg-enabled-management-point-when-theyre-connected-to-the-intranet"></a>Se eu habilitar um CMG, meus clientes se conectarão ao ponto de gerenciamento habilitado para CMG somente quando estiverem conectados à intranet?

Para proteger tráfego confidencial enviado por um CMG, você pode configurar um ponto de gerenciamento HTTPS ou usar HTTP aprimorado.

Se você optar por implantar um CMG e usar certificados PKI para comunicação HTTPS no ponto de gerenciamento habilitado para CMG, selecione a opção para **Permitir clientes somente da internet** nas propriedades do ponto de gerenciamento. Essa configuração garante que os clientes internos continuem a usar os pontos de gerenciamento HTTP em seu ambiente.

Se você usar HTTP aprimorado, não será necessário definir essa configuração. Os clientes continuam a usar HTTP ao se comunicar diretamente com o ponto de gerenciamento habilitado para CMG. Para obter mais informações, confira [HTTP aprimorado](/sccm/core/plan-design/hierarchy/enhanced-http).

## <a name="next-steps"></a>Próximas etapas

- [Plano para o gateway de gerenciamento de nuvem](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway)
- [Configurar o gateway de gerenciamento de nuvem](/sccm/core/clients/manage/cmg/setup-cloud-management-gateway)
- [Certificados para o gateway de gerenciamento de nuvem](/sccm/core/clients/manage/cmg/certificates-for-cloud-management-gateway)
- [Segurança e privacidade para o gateway de gerenciamento de nuvem](/sccm/core/clients/manage/cmg/security-and-privacy-for-cloud-management-gateway)
- [Tamanho e números de escala do gateway de gerenciamento de nuvem](/sccm/core/plan-design/configs/size-and-scale-numbers#bkmk_cmg)
