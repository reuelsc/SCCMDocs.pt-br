---
title: MDM local
titleSuffix: Configuration Manager
description: Saiba mais sobre o gerenciamento de dispositivo móvel local, uma solução de gerenciamento de dispositivo no Configuration Manager
ms.date: 03/05/2019
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 497c05c7-fe9f-4b88-983b-1c5b3d59308e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 49e07a7ebe6ec53d61ea9e2ee3bc941dd8561094
ms.sourcegitcommit: f3dd8405018fe1043434386be15c16752c1a4a3c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/07/2019
ms.locfileid: "57558211"
---
# <a name="on-premises-mdm-in-configuration-manager"></a>MDM local no Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Configuration Manager local gerenciamento de dispositivo móvel (MDM) é uma solução de gerenciamento de dispositivo que utiliza os recursos internos de gerenciamento do sistema operacional do dispositivo. Esse recurso se baseia no padrão de gerenciamento de dispositivo da Open Mobile Alliance (OMA) (DM). Ele usa a infra-estrutura da organização do Configuration Manager para gerenciar e manter os dispositivos. Locais MDM exige o Microsoft Intune Configurar a capacidade de gerenciamento, mas ele só é necessário para a assinatura. Intune é usado às vezes, para ajudar a notificar os dispositivos para fazer check-in para alterações de política, mas ele não é usado para gerenciar dispositivos ou armazenar dados sobre eles.  

![Conceitual local](media/On-premises-conceptual.png)  

O MDM local é diferente do Microsoft Intune, que também se baseia em recursos internos do OMA DM. Todas as funções de gerenciamento no Intune são fornecidas por meio de serviços de nuvem. O MDM local também é diferente da solução de gerenciamento baseado em cliente tradicionalmente oferecida pelo Configuration Manager. Ele utiliza uma infraestrutura semelhante, mas não usa o software cliente instalado separadamente nos dispositivos que ele gerencia.  

> [!Note]  
> Começando na versão 1810, uma conexão do Intune não é mais necessário para novas implantações de MDM local.<!--3607730, fka 1359124--> Sua organização ainda exige licenças do Intune para usar esse recurso. No momento, é possível remover a conexão do Intune de implantações de MDM local existentes. Para obter mais informações, confira a [postagem no blog de suporte do Intune](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/Move-from-Hybrid-Mobile-Device-Management-to-Intune-on-Azure/ba-p/280150).  

A tabela a seguir lista as vantagens e desvantagens do MDM local em comparação com o gerenciamento tradicional baseado em cliente:  

|Vantagens|Desvantagens|  
|----------------|-------------------|  
|**Infraestrutura simplificada** - Menos funções do sistema de sites são necessárias.<br /><br /> **Mais fácil de manter** – porque a funcionalidade de gerenciamento interno do sistema operacional do dispositivo, novas versões do software cliente não são necessárias quando novos recursos de gerenciamento são introduzidos no sistema do Configuration Manager.<br /><br /> **Local** - Todo o gerenciamento e todos os dados são mantidos localmente.|**Menos funcionalidades de gerenciamento de clientes** - Nenhuma orquestração, medição de software, integração de terceiros, sequenciamento de tarefas ou suporte do centro de software.<br /><br /> **Suporte de dispositivo limitado** – atualmente MDM somente dá suporte a dispositivos locais que executam o Windows 10 e Windows 10 Mobile.|  

Os artigos a seguir fornecem informações que você pode usar para planejar, preparar e registrar dispositivos para o MDM local:  

- [Planejamento de MDM local](/sccm/mdm/plan-design/plan-on-premises-mdm)  

    Saiba mais sobre o que considerar ao configurar a infraestrutura do Configuration Manager e planejamento de registro de dispositivo no MDM local.  

- [Etapas de preparação para o MDM local](/sccm/mdm/get-started/preparation-steps-for-on-premises-mdm)  

    Prepare o Configuration Manager para MDM local. Configurar a assinatura do Microsoft Intune, configurar certificados, instalar funções do sistema de site e configurar o registro de dispositivo.  

- [Registrar dispositivos para MDM local](/sccm/mdm/deploy-use/enroll-devices-on-premises-mdm)  

    Saiba mais sobre como o registro ocorre, como os usuários podem registrar seus próprios dispositivos e como registrar dispositivos em massa com um pacote de registro.  

