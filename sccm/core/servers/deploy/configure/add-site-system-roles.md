---
title: Adicionar funções do sistema de sites
titleSuffix: Configuration Manager
description: Entenda as funções do sistema de sites do Configuration Manager e como adicioná-las para ampliar a funcionalidade e a capacidade do seu site.
ms.date: 2/7/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: b90de2d9-494e-43ad-b269-c8ed589f37d3
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 2959d2b97088a2d92b861f0ca4a4d37d0df3e726
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="add-site-system-roles-for-system-center-configuration-manager"></a>Adicionar funções do sistema de sites ao System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Cada site do System Center Configuration Manager é oferece suporte a várias funções do sistema de sites. Cada função amplia a funcionalidade e a capacidade de seu site para fornecer serviços e gerenciar dispositivos e usuários. Cada função de sistema de sites em um servidor de sistema de sites deve ser do mesmo site.   

O Configuration Manager não dá suporte a funções do sistema de sites para vários sites em um único servidor do sistema de sites.  

> [!TIP]  
>  Se não estiver familiarizado com os conceitos básicos das funções do sistema de sites ou com a diferença entre servidor de sites, servidores do sistema de sites e funções do sistema de sites, veja [Aspectos fundamentais do System Center Configuration Manager](../../../../core/understand/fundamentals.md).  

 Os tópicos a seguir detalham os procedimentos e detalhes relacionados para instalação das funções de sistema de sites:  

-   [Instalar funções do sistema de sites no System Center Configuration Manager](../../../../core/servers/deploy/configure/install-site-system-roles.md)  

     Esse tópico fornece orientações básicas sobre como usar os dois assistentes no console, que você pode usar para instalar novas funções do sistema de sites.  

-   [Instalar pontos de distribuição baseados em nuvem no Microsoft Azure para o System Center Configuration Manager](../../../../core/servers/deploy/configure/install-cloud-based-distribution-points-in-microsoft-azure.md)  

    Quando quiser usar o Microsoft Azure para hospedar conteúdo implantado em clientes, as informações nesse tópico ajudarão a configurar os arquivos de certificado necessários para permitir que o Configuration Manager se comunique e use sua assinatura do Microsoft Azure. Além disso, você precisará configurar a resolução de nomes para permitir que os clientes encontrem seus pontos de distribuição baseados em nuvem.  

-   [Instalar funções do sistema de sites para o gerenciamento de dispositivo móvel local no System Center Configuration Manager](../../../../mdm/get-started/install-site-system-roles-for-on-premises-mdm.md)  

     Esse tópico ajudará a configurar com êxito suas funções do sistema de sites para permitir o gerenciamento de dispositivos modernos usando o MDM local do Configuration Manager.  

-   [Configurar opções para funções do sistema de sites para o System Center Configuration Manager](../../../../core/servers/deploy/configure/configuration-options-for-site-system-roles.md)  

     Algumas funções do sistema de sites permitem configurações que exigem mais detalhes do que pode ser explicado na interface do usuário. Esse tópico fornece esses detalhes.  
