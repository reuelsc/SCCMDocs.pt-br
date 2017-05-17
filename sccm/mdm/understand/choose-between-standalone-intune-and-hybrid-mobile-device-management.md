---
title: "Escolher Intune autônomo ou MDM híbrido | Microsoft Docs"
description: "Escolha se deseja implantar o gerenciamento de dispositivo móvel híbrido com o Intune e com o Configuration Manager ou executar o Intune autônomo."
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 73ff9bb9-e605-4b68-92a1-487684fed42d
caps.latest.revision: 10
author: Mtillman
ms.author: mtillman
manager: angrobe
ms.translationtype: Human Translation
ms.sourcegitcommit: 84e3896dd05a8c157f4e94625b0eca60aacc11d3
ms.openlocfilehash: 8f2625aadfd0aed92d9922c7e3c0d3d166a78cdd
ms.contentlocale: pt-br
ms.lasthandoff: 02/25/2017

---
# <a name="choose-between-microsoft-intune-standalone-and-hybrid-mobile-device-management-with-system-center-configuration-manager"></a>Escolha entre o gerenciamento de dispositivo móvel híbrido e independente do Microsoft Intune com o System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Uma das perguntas mais frequentes sobre o MDM (gerenciamento de dispositivo móvel) com o Microsoft Intune é "Devo integrar o Intune ao Configuration Manager (MDM híbrido) ou executar o Intune autônomo na configuração somente em nuvem?" Para responder essa pergunta, você deve comparar cuidadosamente as duas opções e considerar as atualizações do início de 2017 para o Intune autônomo.

## <a name="what-is-intune-standalone"></a>O que é o Intune autônomo?

Intune autônomo é uma solução MDM somente em nuvem que não envolve recursos locais e é gerenciada usando um console Web que pode ser acessado em qualquer lugar do mundo. Os datacenters do Intune são hospedados na América do Norte, Europa e Ásia. Como o Intune é um serviço de nuvem, você pode implantar o gerenciamento do Intune em seus dispositivos em um período de tempo relativamente curto. Você também poderá escolher o Intune autônomo se sua organização estiver mudando para a nuvem.

## <a name="what-is-hybrid-mdm-with-configuration-manager"></a>O que é um MDM híbrido com o Configuration Manager?

MDM híbrido é uma solução que usa o Intune como o canal de entrega de políticas, perfis e aplicativos para dispositivos, mas usa a infraestrutura local do Configuration Manager para armazenar e administrar o conteúdo e gerenciar os dispositivos. Você poderá escolher o MDM híbrido se já tiver um investimento significativo no Configuration Manager e desejar estendê-lo para gerenciar dispositivos móveis. Uma implementação híbrida fornece um controle de "único painel", o que significa que você pode usar a mesma infraestrutura local e o mesmo console administrativo para gerenciar dispositivos móveis com o Intune, e também computadores e servidores com o cliente Configuration Manager tradicional.

## <a name="whats-coming-to-intune-standalone-in-early-2017"></a>Quais serão as novidades do Intune autônomo no início de 2017

Se estiver decidindo entre o autônomo e o híbrido, considere os recursos que entrarão no Intune autônomo no início de 2017. Hoje, o MDM híbrido tem vários recursos avançados que, historicamente, têm o sido o motivo pelo qual alguns clientes optam por gerenciar seus dispositivos com ele e não com o Intune autônomo:

-   Acesso programático (API) – opções de gerenciamento do SDK e do PowerShell.

-   Relatórios personalizados – criar relatórios personalizados.

-   Controle de acesso baseado em função, restringir o acesso a funções administrativas com base em funções atribuídas.

-   Dimensionar – implantar e gerenciar mais de 100 mil dispositivos móveis.

-   Único painel – gerenciar clientes de computadores tradicionais e dispositivos gerenciados pelo Intune usando o mesmo console.

Se você estiver começando a planejar a implantação do Intune hoje e tiver um período de vários meses para pilotos, teste de aceitação e implantação, considere a possibilidade de escolher o Intune autônomo agora, entendendo que as novas atualizações para o serviço de nuvem incluirão mais funcionalidades. Durante o primeiro semestre do ano civil 2017, o Intune autônomo receberá atualizações que fornecem grande parte das funcionalidades avançadas de uma implantação híbrida com o Configuration Manager. O Intune autônomo logo passará para a plataforma de nuvem Microsoft Azure e isso trará melhorias de escalabilidade, acesso baseado em função por meio do Portal do Azure, relatórios personalizados e acesso programático por meio da API do Graph do Azure.

Você pode mudar de híbrido para Intune autônomo ou de autônomo para híbrido, mas isso requer ajuda de operações e do Suporte da Microsoft. Para isso também será necessário cancelar o registro e registrar novamente todos os dispositivos depois que a autoridade de gerenciamento for alterada.  A Microsoft está trabalhando para melhorar a experiência com as mudanças de configurações em uma atualização futura do serviço.

