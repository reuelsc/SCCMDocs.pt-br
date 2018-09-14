---
title: Escolher Intune autônomo ou MDM híbrido
titleSuffix: Configuration Manager
description: Escolha se deseja implantar o gerenciamento de dispositivo móvel híbrido com o Intune e com o Configuration Manager ou executar o Intune autônomo.
ms.date: 08/14/2018
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 73ff9bb9-e605-4b68-92a1-487684fed42d
author: aczechowski
ms.author: aaroncz
manager: dougeby
robots: noindex,nofollow
ms.openlocfilehash: 153c1208cef8a940cc06412322e8112d53d17e58
ms.sourcegitcommit: 98c3f7848dc9014de05541aefa09f36d49174784
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/14/2018
ms.locfileid: "42584440"
---
# <a name="choose-between-microsoft-intune-standalone-and-hybrid-mdm-with-configuration-manager"></a>Escolha entre o Microsoft Intune autônomo e o MDM híbrido com o Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Uma das perguntas mais frequentes sobre o MDM (gerenciamento de dispositivo móvel) com o Microsoft Intune é "Devo integrar o Intune ao Configuration Manager (MDM híbrido) ou executar o Intune autônomo na configuração somente em nuvem?" 

O Intune no Azure é a solução de MDM recomendada pela Microsoft.     


> [!Important]  
> A partir de 14 de agosto de 2018, o gerenciamento híbrido de dispositivos móveis é um [recurso preterido](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures). Para saber mais, confira [O que é o MDM híbrido](/sccm/mdm/understand/hybrid-mobile-device-management).<!--Intune feature 2683117-->  


 
## <a name="intune-standalone"></a>Intune autônomo

O Intune autônomo é a topologia de implantação recomendada da Microsoft. O Intune autônomo é uma solução de MDM que você gerencia usando um console Web que pode ser acessado de qualquer lugar do mundo. Os datacenters do Intune são hospedados na América do Norte, na Europa e na Ásia. Como o Intune é um serviço de nuvem, você pode implantar rapidamente o gerenciamento do Intune em seus dispositivos.

Os clientes geralmente acham mais rápido e fácil implantar a topologia autônoma, porque não há dependências de componentes locais. O Intune autônomo agora está na plataforma na nuvem do Microsoft Azure e oferece muitos recursos avançados, como:  

- Plataforma de gerenciamento de mobilidade corporativa integrada: uma experiência de administrador e de plataforma na nuvem integrada no Portal do Azure para Intune, Azure AD Premium e Proteção de Informações do Azure  

- Gerenciamento de dispositivo móvel: recursos avançados de proteção de informações e gerenciamento de dispositivos móveis  

- Dimensionar: implante e gerencie dispositivos móveis sem se preocupar com o dimensionamento  

- Controle de acesso baseado em função: restrinja o acesso a funções administrativas com base em funções e escopos atribuídos  

- Acesso programático (API): suporte à API do Microsoft Graph e opções de gerenciamento com SDK e PowerShell  

- Console Web: um console baseado em HTML 5 criado de acordo com padrões da Web compatível com os mais modernos navegadores da Web  

- Relatórios avançados: capacidade de criar relatórios personalizados  

- Agilidade: configuração simples e fornecimento rápido de novos recursos  



## <a name="hybrid-mdm-with-configuration-manager"></a>MDM híbrido com o Configuration Manager

> [!Important]  
> A partir de 14 de agosto de 2018, o gerenciamento híbrido de dispositivos móveis é um [recurso preterido](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures). Para saber mais, confira [O que é o MDM híbrido](/sccm/mdm/understand/hybrid-mobile-device-management).  

O MDM híbrido é uma solução que integra recursos de gerenciamento de dispositivos móveis do Intune ao Configuration Manager. Ele usa o Intune como o canal de entrega de políticas, perfis e aplicativos para dispositivos, mas usa a infraestrutura local do Configuration Manager para administrar o conteúdo e gerenciar os dispositivos. Uma implantação híbrida lhe dá controle a partir de um "único painel". Isso significa que você pode usar a mesma infraestrutura local e console administrativo para gerenciar dispositivos móveis com o Intune, bem como PCs e servidores com o cliente tradicional do Configuration Manager. 

Você pode escolher o MDM híbrido pelos seguintes motivos:  

- Você deseja gerenciar os dispositivos móveis inscritos no Intune e dispositivos gerenciados com o cliente do Configuration Manager a partir do mesmo console administrativo  

- Sua infraestrutura exige que você tenha vários servidores NDES para fornecimento de certificado para dispositivos móveis  

- Sua infraestrutura exige que você tenha vários conectores do Exchange  

- Você requer suporte a criptografia S/MIME

> [!Note]  
> Se você configurar o MDM híbrido no Configuration Manager para acesso condicional com o Exchange no local, os usuários ainda poderão acessar o email no Outlook para iOS e Android. Essa mesma configuração com o Intune autônomo bloqueia o email para esses clientes.<!--Intune bug 2285890-->  



## <a name="change-the-mdm-authority"></a>Alterar a autoridade de MDM

Se precisar alterar a configuração da autoridade MDM, você pode alterá-la por conta própria sem precisar entrar em contato com o Suporte da Microsoft e sem a necessidade de cancelar o registro e registrar novamente os dispositivos gerenciados existentes. Para obter detalhes, veja [Alterar sua autoridade de MDM](/sccm/mdm/deploy-use/change-mdm-authority).

