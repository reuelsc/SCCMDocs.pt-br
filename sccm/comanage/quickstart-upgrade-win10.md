---
title: Atualizar para o Windows 10
titleSuffix: Configuration Manager
description: Atualize dispositivos para Windows 10 versão 1709 ou posterior, o que é necessário para o cogerenciamento
ms.date: 01/14/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 561eb5b6-f90c-485a-91c2-e45bb0ce7877
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: bbc042975840e5b4e840928f01257785f4859dd4
ms.sourcegitcommit: 18ad7686d194d8cc9136a761b8153a1ead1cdc6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/23/2019
ms.locfileid: "66176835"
---
# <a name="upgrade-windows-10-for-co-management"></a>Atualizar o Windows 10 para o cogerenciamento

Conforme você trabalha para integrar sua organização ao cogerenciamento, manter-se atualizado é um obstáculo significativo para alguns clientes. O cogerenciamento requer o [Windows 10 versão 1709](https://docs.microsoft.com/windows/whats-new/whats-new-windows-10-version-1709) ou posterior. Depois de atualizar o Windows e configurar o registro automático, os clientes serão inscritos automaticamente no cogerenciamento.

No vídeo a seguir, o gerente de programas sênior Rob York e o gerente de marketing de produtos Locky Ainley discutem e demonstram a atualização para o Windows 10 para o cogerenciamento:

> [!VIDEO https://channel9.msdn.com/Series/Endpoint-Zone/Upgrading-to-Windows-10-to-Enable-Co-Management/player]



## <a name="why-upgrade"></a>Por que atualizar?

Entre outras melhorias de plataforma, o Windows 10 versão 1709 e posterior dá suporte ao registro automático. Esse comportamento faz com que um dispositivo seja inscrito automaticamente no Intune quando ingressado no Azure Active Directory (Azure AD). 

Para saber mais, confira [Habilitar o registro automático no Windows 10](https://docs.microsoft.com/intune/windows-enroll#enable-windows-10-automatic-enrollment).


## <a name="how-to-do-it"></a>Como fazer isso

Veja algumas dicas que aprendemos com a ajuda de milhares de clientes para se atualizar rapidamente:

- Use implantações em fases para implantar essa atualização para as pessoas certas nos momentos certos. Saiba mais em [Criar implantações em fases](/sccm/osd/deploy-use/create-phased-deployment-for-task-sequence).  

- Use o pré-armazenamento em cache para reduzir os tempos de espera do usuário. Para saber mais, confira [Configurar o conteúdo de armazenamento prévio em cache](/sccm/osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system#configure-pre-cache-content).  

- Use o modelo de sequência de tarefas de atualização in-loco padrão. Em seguida, configure suas etapas de pré e pós-atualização e as ações em caso de falha. Para saber mais, confira [Etapas de sequência de tarefas recomendadas para pós-processamento](/sccm/osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system#recommended-task-sequence-steps-for-post-processing).  

- Se seu ambiente tem uma força de trabalho altamente móvel, o Configuration Manager dá suporte à atualização in-loco por meio do gateway de gerenciamento de nuvem (CMG). Esse recurso permite atualizar os clientes do Windows 10 quando eles são baseados na Internet. Para saber mais sobre o CMG, confira [](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway).  

- Oferece a opção de cogerenciamento para os usuários que desejam ser pioneiros. Essa abordagem acelera a adoção inicial. Ao identificar essas pessoas com antecedência, você pode garantir uma boa cobertura no início de uma distribuição. Você também recebe validação e feedback de usuários satisfeitos com as mudanças e interessados em lançamentos mais frequentes. Programas de usuários pioneiros geram interesse em novas tecnologias e crescem ao longo do tempo.  


## <a name="case-studies"></a>Estudos de caso

A Microsoft IT implantou o Windows 10 para 96.000 usuários distribuídos na Microsoft. A implantação incluiu usuários remotos e usuários da rede corporativa. A implantação foi concluída em nove semanas. Para saber mais sobre a experiência deles, confira [Implantação do Windows 10 na Microsoft como uma atualização in-loco](https://www.microsoft.com/itshowcase/deploying-windows-10-at-microsoft-as-an-in-place-upgrade).  

Um grande fabricante europeu de software usa com sucesso um grupo de usuários pioneiros. Após os grupos iniciais de teste e piloto, aproximadamente 2.000 funcionários recebem a primeira atualização, upgrades e software. Esse grupo inclui equipe de TI e voluntários. Esse nível de envolvimento com seus usuários proporciona a eles um nível maior de confiança ao testar e mais credibilidade quando os lançamentos em massa começam.



## <a name="contact-fasttrack"></a>Entre em contato com o FastTrack

Se você precisar de ajuda com sua atualização do Windows 10 em qualquer ponto do processo, vá para o [Microsoft FastTrack](https://Microsoft.com/FastTrack/), entre e solicite assistência. 

Para saber mais, confira [Obter ajuda do FastTrack](/sccm/comanage/quickstart-fasttrack). 

