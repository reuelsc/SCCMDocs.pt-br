---
title: Configurar Endpoint Protection
titleSuffix: Configuration Manager
description: Saiba como configurar o Configuration Manager para atualizar e distribuir as definições de malware do Windows Defender.
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: e63f2394-6eb1-4a33-bec5-8377fc62a34e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 89eee933d9845ae86bcc8d008045b669d104d03d
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56156722"
---
# <a name="configure-endpoint-protection"></a>Configurar Endpoint Protection

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Antes de usar o Endpoint Protection para gerenciar a segurança e o malware em computadores cliente do Configuration Manager, execute as etapas de configuração detalhadas neste artigo.  

## <a name="how-to-configure-endpoint-protection-in-configuration-manager"></a>Como configurar o Endpoint Protection no Configuration Manager  
 O Endpoint Protection no Configuration Manager tem dependências externas e dependências dentro do produto.  

### <a name="steps-to-configure-endpoint-protection-in-configuration-manager"></a>Etapas para configurar o Endpoint Protection no Configuration Manager  
 Use a tabela a seguir que contém etapas, detalhes e mais informações sobre como configurar o Endpoint Protection.  

> [!IMPORTANT]  
>  Se você gerencia o endpoint protection para computadores Windows 10, configure o Configuration Manager para atualizar e distribuir as definições de malware para o Windows Defender. O Windows Defender está incluído no Windows 10, mas o SCEPInstall ainda deve ser instalado e as configurações de cliente personalizadas para o Endpoint Protection (**Etapa 5** abaixo) ainda são necessárias. </br> </br>
> A partir do Configuration Manager 1802, os dispositivos Windows 10 não precisam ter o agente do Endpoint Protection (SCEPInstall) instalado. Se ele já estiver instalado nos dispositivos Windows 10, o Configuration Manager não o removerá. Os administradores podem remover o agente do Endpoint Protection dos dispositivos Windows 10 que executam, no mínimo, a versão de cliente 1802. O SCEPInstall.exe ainda pode estar presente no C:\Windows\ccmsetup em alguns computadores, mas não deve ser baixado em novas instalações de cliente. As configurações personalizadas do cliente para o Endpoint Protection (**Etapa 5** abaixo) ainda são necessárias. <!--503654-->

|Etapas|Detalhes|  
|-----------|-------------|  
|**Etapa 1:** [Criar uma função do sistema de sites do ponto do Endpoint Protection](endpoint-protection-site-role.md)|A função do sistema de sites do ponto do Endpoint Protection deve ser instalada antes que você possa usar o Endpoint Protection. Ela deve estar instalada em apenas um servidor do sistema de sites e deve estar instalada no topo da hierarquia em um site de administração central ou em um site primário autônomo. |  
|**Etapa 2:** [Configurar alertas para o Endpoint Protection](endpoint-configure-alerts.md)|Os alertas informam o administrador quando eventos específicos ocorrem, como no caso de uma infecção por malware. Os alertas são exibidos no nó **Alertas** do workspace **Monitoramento** ou, como opção, podem ser enviados por email para usuários especificados. |  
|**Etapa 3:** [Configurar atualizações de definição para o Endpoint Protection](endpoint-definition-updates.md)|O Endpoint Protection pode ser configurado para usar várias origens para baixar atualizações de definições. |  
|**Etapa 4:** [Configurar a política antimalware padrão e criar políticas antimalware personalizadas](endpoint-antimalware-policies.md)|A política antimalware padrão é aplicada quando o cliente do Endpoint Protection está instalado. As políticas personalizadas que você implantou são aplicadas por padrão até 60 minutos após a implantação do cliente. Verifique se você configurou políticas antimalware antes de implantar o cliente Endpoint Protection. |  
|**Etapa 5:** [Definir configurações personalizadas do cliente para o Endpoint Protection](endpoint-protection-configure-client.md)|Use configurações personalizadas do cliente para definir as configurações do Endpoint Protection para coleções de computadores em sua hierarquia.<br /><br /> Observações: não defina as configurações do cliente padrão do Endpoint Protection, a menos que tenha certeza de que deseja aplicá-las a todos os computadores na hierarquia. |  
