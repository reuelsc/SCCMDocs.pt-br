---
title: Perguntas frequentes sobre o CMG
description: Use este artigo para responder a perguntas frequentes sobre o gateway de gerenciamento de nuvem
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 03/22/2018
ms.topic: article
ms.prod: configuration-manager
ms.technology:
- configmgr-other
ms.assetid: 4c1a128d-22fb-49f1-8e0b-36513a8dc117
ms.openlocfilehash: 8615b28735165650a0ec25e3d3114263835803d6
ms.sourcegitcommit: 11bf4ed40ed0cbb10500cc58bbecbd23c92bfe20
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/23/2018
---
# <a name="frequently-asked-questions-about-the-cloud-management-gateway"></a>Perguntas frequentes sobre o gateway de gerenciamento de nuvem

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Este artigo responde às perguntas frequentes sobre o gateway de gerenciamento de nuvem. Para obter mais informações, consulte [Planejar o gateway de gerenciamento de nuvem](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway).


## <a name="frequently-asked-questions"></a>Perguntas frequentes

### <a name="what-certificates-do-i-need"></a>Quais certificados são necessários?

Para obter informações mais detalhadas, consulte [Certificados do gateway de gerenciamento de nuvem](/sccm/core/clients/manage/cmg/certificates-for-cloud-management-gateway).


### <a name="do-i-need-azure-expressroute"></a>O Azure ExpressRoute é necessário?

O [Azure ExpressRoute](/azure/expressroute/expressroute-introduction) possibilita que você estenda a rede local para a nuvem da Microsoft. O ExpressRoute, ou outras conexões de rede virtual desse tipo, não é necessário para o gateway de gerenciamento de nuvem do Configuration Manager. O design do gateway de gerenciamento de nuvem permite que os clientes baseados na Internet se comuniquem por meio do serviço do Azure com os sistemas de sites locais sem nenhuma configuração de rede adicional. Para obter mais informações, consulte [Planejar o gateway de gerenciamento de nuvem](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway)

Caso sua organização use o ExpressRoute, uma melhor prática de segurança é isolar a assinatura do Azure para o gateway de gerenciamento de nuvem. Essa configuração garante que o serviço de gateway de gerenciamento de nuvem não está conectado acidentalmente dessa maneira. Para obter mais informações, consulte [Segurança e privacidade do gateway de gerenciamento de nuvem](/sccm/core/clients/manage/cmg/security-and-privacy-for-cloud-management-gateway).


### <a name="do-i-need-to-maintain-the-azure-virtual-machines"></a>É necessário manter as máquinas virtuais do Azure?

Nenhuma manutenção é necessária. O design do gateway de gerenciamento de nuvem usa o PaaS (plataforma como serviço) do Azure. Usando a assinatura fornecida, o Configuration Manager cria as VMs (máquinas virtuais), o armazenamento e a rede necessários. O Azure protege e atualiza a máquina virtual. Essas VMs não fazem parte do ambiente local, como é o caso do IaaS (infraestrutura como serviço). O gateway de gerenciamento de nuvem é um PaaS que estende o ambiente do Configuration Manager para a nuvem. 


### <a name="im-already-using-ibcm-if-i-add-cmg-how-do-clients-behave"></a>Já estou usando o IBCM. Se eu adicionar o CMG, como os clientes se comportarão?

Se você já implantou o [IBCM](/sccm/core/clients/manage/plan-internet-based-client-management) (gerenciamento de clientes baseado na Internet), implante também o gateway de gerenciamento de nuvem. Os clientes recebem a política para ambos os serviços. Conforme eles usam um perfil móvel na Internet, eles aleatoriamente selecionam e usam um desses serviços baseados na Internet.


## <a name="next-steps"></a>Próximas etapas

- [Plano para o gateway de gerenciamento de nuvem](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway)
- [Configurar o gateway de gerenciamento de nuvem](/sccm/core/clients/manage/cmg/setup-cloud-management-gateway)
- [Certificados para o gateway de gerenciamento de nuvem](/sccm/core/clients/manage/cmg/certificates-for-cloud-management-gateway)
- [Segurança e privacidade para o gateway de gerenciamento de nuvem](/sccm/core/clients/manage/cmg/security-and-privacy-for-cloud-management-gateway)
- [Tamanho e números de escala do gateway de gerenciamento de nuvem](/sccm/core/plan-design/configs/size-and-scale-numbers#bkmk_cmg)