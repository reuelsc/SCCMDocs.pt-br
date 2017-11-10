---
title: "Escolher Intune autônomo ou MDM híbrido"
titleSuffix: Configuration Manager
description: "Escolha se deseja implantar o gerenciamento de dispositivo móvel híbrido com o Intune e com o Configuration Manager ou executar o Intune autônomo."
ms.custom: na
ms.date: 07/18/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 73ff9bb9-e605-4b68-92a1-487684fed42d
caps.latest.revision: "10"
author: dougeby
ms.author: dougeby
manager: angrobe
ms.openlocfilehash: 993a3ada8b887adb52be468ea4e936140a455bca
ms.sourcegitcommit: c236214b2fcc13dae7bad96d7fb33f692868191d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2017
---
# <a name="choose-between-microsoft-intune-standalone-and-hybrid-mobile-device-management-with-system-center-configuration-manager"></a>Escolha entre o gerenciamento de dispositivo móvel híbrido e independente do Microsoft Intune com o System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Uma das perguntas mais frequentes sobre o MDM (gerenciamento de dispositivo móvel) com o Microsoft Intune é "Devo integrar o Intune ao Configuration Manager (MDM híbrido) ou executar o Intune autônomo na configuração somente em nuvem?" Para responder essa pergunta, você deve comparar com atenção as duas opções.
 
## <a name="intune-standalone"></a>Intune autônomo
O Intune autônomo é a topologia de implantação recomendada da Microsoft. O Intune autônomo é uma solução MDM somente em nuvem e é gerenciada usando um console Web que pode ser acessado em qualquer lugar do mundo. Os datacenters do Intune são hospedados na América do Norte, Europa e Ásia. Como o Intune é um serviço de nuvem, você pode implantar o gerenciamento do Intune em seus dispositivos em um período de tempo relativamente curto.

Os clientes geralmente acham mais rápido e fácil implantar a topologia autônoma, porque não há nenhuma dependência para componentes locais. O Intune autônomo agora está na plataforma na nuvem do Microsoft Azure e oferece muitos recursos avançados, como:
- Plataforma de gerenciamento de mobilidade corporativa integrada – uma experiência de administrador e de plataforma na nuvem integrada no Portal do Azure para Intune, Azure AD Premium e Proteção de Informações do Azure.
- Gerenciamento de dispositivo móvel – recursos de proteção de informações e gerenciamento de dispositivos móveis avançado.
- Dimensionar – Implante e gerencie dispositivos móveis sem se preocupar em dimensionar.
- Controle de acesso baseado em função – Restrinja o acesso a funções administrativas com base em funções e escopos atribuídos.
- Acesso programático (API) – Suporte a API do Microsoft Graph e opções de gerenciamento do SDK e do PowerShell.
- Console Web – Um console baseado em HTML 5 criado de acordo com padrões da Web com suporte para os mais modernos navegadores da Web.
- Relatórios avançados – Capacidade de criar relatórios personalizados.
- Agilidade – Configuração simples e fornecimento rápido de novos recursos.


## <a name="hybrid-mdm-with-configuration-manager"></a>MDM híbrido com o Configuration Manager
O MDM híbrido é uma solução que integra recursos de gerenciamento de dispositivos móveis do Intune ao Configuration Manager. Ele usa o Intune como o canal de entrega de políticas, perfis e aplicativos para dispositivos, mas usa a infraestrutura local do Configuration Manager para administrar o conteúdo e gerenciar os dispositivos. Uma implantação híbrida lhe dá controle a partir de um "único painel".  Isso significa que você pode usar a mesma infraestrutura local e console administrativo para gerenciar dispositivos móveis com o Intune, bem como PCs e servidores com o cliente tradicional do Configuration Manager. Você pode escolher o MDM híbrido pelos seguintes motivos:  
- Você deseja gerenciar os dispositivos móveis inscritos no Intune e dispositivos gerenciados com o cliente do Configuration Manager a partir do mesmo console administrativo
- Sua infraestrutura exige que você tenha vários servidores NDES para fornecimento de certificado para dispositivos móveis
- Sua infraestrutura exige que você tenha vários conectores do Exchange
- Você requer suporte a criptografia S/MIME


## <a name="changing-the-mdm-authority-setting"></a>Alterar a configuração da autoridade MDM
Se precisar alterar a configuração da autoridade MDM, você pode alterá-la por conta própria sem precisar entrar em contato com o Suporte da Microsoft e sem a necessidade de cancelar o registro e registrar novamente os dispositivos gerenciados existentes. Para obter detalhes, veja [Alterar sua autoridade de MDM](../deploy-use/change-mdm-authority.md).

> [!NOTE]    
> Você deve ter o Configuration Manager versão 1610 ou superior para alterar a sua autoridade MDM para o Intune autônomo. Quando você tem uma versão anterior do Configuration Manager, é possível alterar a autoridade MDM, mas ele requer ajuda de operações e suporte da Microsoft. Ele também requer que você cancele o registro e registre novamente todos os seus dispositivos após a alteração da autoridade MDM.  
