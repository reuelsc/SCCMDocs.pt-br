---
title: Atualizar o Windows 10
titleSuffix: Configuration Manager
description: Atualizar dispositivos Windows 10 versão 1709 ou posterior, que é necessário para o cogerenciamento
ms.date: 01/14/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 561eb5b6-f90c-485a-91c2-e45bb0ce7877
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 0815a974f3b1f29f664a2948eed33de24c6ecff3
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56754546"
---
# <a name="upgrade-windows-10-for-co-management"></a>Atualizar o Windows 10 para cogerenciamento

Conforme você trabalha em direção a integração sua organização para o cogerenciamento, obtendo atual é uma barreira significativa para alguns clientes. Requer o cogerenciamento [Windows 10 versão 1709](https://docs.microsoft.com/windows/whats-new/whats-new-windows-10-version-1709) ou posterior. Depois de atualizar o Windows e configurar o registro automático, os clientes são registrados automaticamente para o cogerenciamento.

No vídeo a seguir, gerente de programa sênior Rob York e Ainley Locky do gerente de marketing de produto discutem e atualizando para o Windows 10 para cogerenciamento de demonstração:

> [!VIDEO https://channel9.msdn.com/Series/Endpoint-Zone/Upgrading-to-Windows-10-to-Enable-Co-Management/player]



## <a name="why-upgrade"></a>Por que atualizar?

Entre outros aprimoramentos de plataforma, o Windows 10 versão 1709 e posterior dá suporte a registro automático. Esse comportamento faz com que um dispositivo registrar automaticamente para o Intune, quando ele ingressado no Azure Active Directory (Azure AD). 

Para obter mais informações, consulte [registro automático de habilitar o Windows 10](https://docs.microsoft.com/intune/windows-enroll#enable-windows-10-automatic-enrollment).


## <a name="how-to-do-it"></a>Como fazer isso

Aqui estão algumas dicas que aprendemos com a Ajuda milhares de clientes atual rapidamente:

- Use implantações em fases para implementar essa atualização para as pessoas certas na direita vezes. Saiba mais em [Criar implantações em fases](/sccm/osd/deploy-use/create-phased-deployment-for-task-sequence).  

- Use o pré-armazenamento em cache para reduzir os tempos de espera do usuário. Para saber mais, confira [Configurar o conteúdo de armazenamento prévio em cache](/sccm/osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system#configure-pre-cache-content).  

- Use o modelo de sequência de tarefas de atualização no local padrão. Em seguida, configure suas etapas de pré e pós-atualização e as ações de falha. Para obter mais informações, consulte [recomendado etapas de sequência de tarefas para o pós-processamento](/sccm/osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system#recommended-task-sequence-steps-for-post-processing).  

- Se seu ambiente tem uma força de trabalho altamente móvel, o Configuration Manager dá suporte à atualização no local por meio do gateway de gerenciamento de nuvem (CMG). Esse recurso permite que você atualize seus clientes Windows 10 quando eles são baseados na internet. Para obter mais informações sobre o CMG, consulte [ ](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway).  

- Oferece um opt-in para o cogerenciamento para os usuários que desejam ser pioneiros. Essa abordagem acelera a adoção inicial. Ao identificar essas pessoas com antecedência, você pode tornar claro que uma boa cobertura no início de uma distribuição. Você também receber comentários e validação de usuários que estão interessados em versões mais frequentes e satisfeito com a alteração. Programas de adoção antecipada geram interesse em novas tecnologias e crescem em tamanho ao longo do tempo.  


## <a name="case-studies"></a>Estudos de caso

Microsoft IT implantar o Windows 10 para usuários distribuídos 96,000 na Microsoft. A implantação incluído usuários remotos e os usuários na rede corporativa. A implantação foi concluída em nove semanas. Para obter mais informações sobre sua experiência, consulte [Implantando o Windows 10 na Microsoft, como uma atualização in loco](https://www.microsoft.com/download/details.aspx?id=50377).  

Com êxito, um fabricante de software europeus grandes usa um grupo de adoção antecipada. Depois de testar inicial e um piloto de grupos, aproximadamente 2.000 funcionários recebem a primeira atualização, atualizações e software. Esse grupo inclui a equipe de TI e inscreva-se no voluntários. Esse nível de engajamento com seus usuários dá a eles um maior nível de confiança ao testar e mais credibilidade quando começam a distribuições em massa.



## <a name="contact-fasttrack"></a>Entre em contato com o FastTrack

Se você precisar de assistência com a atualização do Windows 10 em qualquer ponto no processo, acesse [Microsoft FastTrack](https://Microsoft.com/FastTrack/), entrar e solicitar assistência. 

Para obter mais informações, consulte [Obtenha ajuda do FastTrack](/sccm/comanage/quickstart-fasttrack). 

