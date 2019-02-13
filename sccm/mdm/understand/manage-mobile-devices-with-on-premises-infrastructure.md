---
title: MDM (Gerenciamento de dispositivos móveis) local
titleSuffix: Configuration Manager
description: Conheça o Gerenciamento de Dispositivo Móvel Local, uma solução de gerenciamento de dispositivos no System Center Configuration Manager.
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 497c05c7-fe9f-4b88-983b-1c5b3d59308e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 63a82c6b81d5a2e09c6f73b79c39372c96ed4e07
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56143649"
---
# <a name="on-premises-mobile-device-management-mdm-in-system-center-configuration-manager"></a>MDM (Gerenciamento de Dispositivo Móvel) Local no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

O Gerenciamento de Dispositivo Móvel Local do System Center Configuration Manager é uma solução de gerenciamento de dispositivos que utiliza os recursos internos de gerenciamento dos sistemas operacionais dos dispositivos (baseados no padrão OMA DM ou Gerenciamento de Dispositivo da Open Mobile Alliance) e usa infraestrutura do Configuration Manager da empresa para gerenciar e manter os dispositivos. O Gerenciamento de Dispositivo Móvel Local exige o Microsoft Intune para configurar a capacidade de gerenciamento, mas só é necessário para a assinatura (e, às vezes, para ajudar a notificar os dispositivos a fazerem check-in para alterações de política), contudo ele não é usado para gerenciar os dispositivos ou armazenar dados sobre eles.  

 ![Conceitual local](media/On-premises-conceptual.png)  

 O Gerenciamento de Dispositivo Móvel Local é diferente do Microsoft Intune, que também utiliza os recursos internos do OMA DM, mas em que todas as funções de gerenciamento são entregues por meio de serviços de nuvem.  O Gerenciamento de Dispositivo Móvel Local também é diferente da solução de gerenciamento baseada em cliente tradicionalmente oferecida pelo Configuration Manager, em que ele utiliza uma infraestrutura corporativa semelhante, mas não usa um software cliente instalado separadamente nos computadores e dispositivos que ele gerencia.  

 A tabela abaixo lista as vantagens e desvantagens do Gerenciamento de Dispositivo Móvel Local em comparação com o gerenciamento tradicional baseado em cliente:  

|Vantagens|Desvantagens|  
|----------------|-------------------|  
|**Infraestrutura simplificada** - Menos funções do sistema de sites são necessárias.<br /><br /> **Manutenção mais fácil** – Como a funcionalidade de gerenciamento é inserida no sistema operacional do dispositivo, novas versões do software cliente não são necessárias quando novos recursos de gerenciamento são introduzidos no sistema do Configuration Manager.<br /><br /> **Local** - Todo o gerenciamento e todos os dados são mantidos localmente.|**Menos funcionalidades de gerenciamento de clientes** - Nenhuma orquestração, medição de software, integração de terceiros, sequenciamento de tarefas ou suporte do centro de software.<br /><br /> **Suporte de dispositivo limitado** – Atualmente, o Gerenciador de Dispositivo Móvel Local dá suporte apenas a dispositivos que executam o Windows 10 e Windows 10 Mobile.|  

 Os seguintes tópicos fornecem informações que podem ser usadas para planejar, preparar e registrar dispositivos para o Gerenciamento de Dispositivo Móvel Local:  

-   [Planejar o Gerenciamento de Dispositivo Móvel Local no System Center Configuration Manager](../plan-design/plan-on-premises-mdm.md)  

     Saiba mais sobre o que deve ser considerado ao configurar a infraestrutura do Configuration Manager e planejar o registro de dispositivo no Gerenciamento de Dispositivo Móvel Local.  

-   [Etapas de preparação para o Gerenciamento de Dispositivo Móvel Local no System Center Configuration Manager](../get-started/preparation-steps-for-on-premises-mdm.md)  

     Saiba mais sobre como preparar o sistema do Configuration Manager para o Gerenciamento de Dispositivo Móvel Local configurando a assinatura do Microsoft Intune, configurando certificados, instalando funções do sistema de sites e configurando o registro do dispositivo.  

-   [Registrar dispositivos para o gerenciamento de dispositivo móvel local no System Center Configuration Manager](../deploy-use/enroll-devices-on-premises-mdm.md)  

     Saiba mais sobre como o registro ocorre, como os usuários podem registrar seus próprios dispositivos e como registrar dispositivos em massa com um pacote de registro.  
