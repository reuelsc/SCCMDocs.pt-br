---
title: Preparar para o MDM local
titleSuffix: Configuration Manager
description: Preparar para gerenciar dispositivos com gerenciamento de dispositivo móvel local no Configuration Manager
ms.date: 03/05/2019
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 1ef60106-8f31-46d6-95a6-25a6495f22c7
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: fad5ce96b84b5a6edfafdead64cff0223009ebf8
ms.sourcegitcommit: f3dd8405018fe1043434386be15c16752c1a4a3c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/07/2019
ms.locfileid: "57558041"
---
# <a name="preparation-steps-for-on-premises-mdm-in-configuration-manager"></a>Etapas de preparação para o MDM local no Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Para gerenciar dispositivos com gerenciamento de dispositivo móvel local do Configuration Manager (MDM), primeiro configurar a infraestrutura necessária. As funções do sistema de sites necessárias precisam se comunicar por um canal confiável com os dispositivos móveis. Essas funções incluem o ponto proxy do registro, o ponto de registro, o ponto de gerenciamento de dispositivo e o ponto de distribuição.

As seguintes tarefas de alto nível são necessárias para preparar o Configuration Manager para MDM local:  

- [Configurar uma assinatura do Microsoft Intune para MDM local](/sccm/mdm/get-started/set-up-intune-subscription-on-premises-mdm)  

    Inscreva-se no Microsoft Intune e, em seguida, adicione a assinatura ao Configuration Manager por meio do console do Configuration Manager. Essa etapa é necessária para fins de licenciamento. Intune não é usado para gerenciar os dispositivos ou armazenar informações de gerenciamento. Toda coordenação e gerenciamento de dispositivos está com a iniciativa da sua organização usando a infraestrutura local do Configuration Manager.  

    > [!Note]  
    > Começando na versão 1810, uma conexão do Intune não é mais necessário para novas implantações de MDM local.<!--3607730, fka 1359124--> Sua organização ainda exige licenças do Intune para usar esse recurso. No momento, é possível remover a conexão do Intune de implantações de MDM local existentes. Para obter mais informações, confira a [postagem no blog de suporte do Intune](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/Move-from-Hybrid-Mobile-Device-Management-to-Intune-on-Azure/ba-p/280150).  

- [Instalar funções do sistema de site para o MDM local](/sccm/mdm/get-started/install-site-system-roles-for-on-premises-mdm)  

    Instalar e configurar os sistemas de site necessários para gerenciar dispositivos com a infraestrutura do Configuration Manager local. No mínimo, este recurso requer o ponto proxy do registro, ponto de registro, ponto de gerenciamento de dispositivo e as funções de ponto de distribuição.  

- [Configurar certificados para comunicações confiáveis de MDM local](/sccm/mdm/get-started/set-up-certificates-on-premises-mdm)  

    Configure a infraestrutura do Configuration Manager local para permitir comunicações confiáveis (HTTPS) entre os dispositivos gerenciados e os servidores que hospedam as funções do sistema de sites necessárias.  

- [Configurar o registro de dispositivo para MDM local](/sccm/mdm/get-started/set-up-device-enrollment-on-premises-mdm)  

    Conceder permissão aos usuários para registrar computadores e dispositivos. Instale o certificado raiz confiável nos dispositivos para permitir conexões HTTPS para servidores do sistema de site. Esses dispositivos normalmente não são ingressados no domínio.  

