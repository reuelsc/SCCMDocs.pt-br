---
title: Configurar o Endpoint Protection | Microsoft Docs
description: "Saiba como configurar o Configuration Manager para atualizar e distribuir as definições de malware do Windows Defender."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: e63f2394-6eb1-4a33-bec5-8377fc62a34e
caps.latest.revision: 21
author: NathBarn
ms.author: nathbarn
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 180d05d3493f8c4288ad4bf640da15bd599c2072
ms.openlocfilehash: 783d8352e3e1f06af3a5d8534b4fa811f36fdc17


---

# <a name="configure-endpoint-protection-in-system-center-configuration-manager"></a>Configurar o Endpoint Protection no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Antes de usar o Endpoint Protection para gerenciar a segurança e malware em computadores cliente do Configuration Manager, você deve executar as etapas de configuração detalhadas neste tópico.  

## <a name="how-to-configure-endpoint-protection-in-configuration-manager"></a>Como configurar o Endpoint Protection no Configuration Manager  
 O Endpoint Protection no Configuration Manager tem dependências externas e dependências dentro do produto.  

### <a name="steps-to-configure-endpoint-protection-in-configuration-manager"></a>Etapas para configurar o Endpoint Protection no Configuration Manager  
 Use a tabela a seguir que contém etapas, detalhes e mais informações sobre como configurar o Endpoint Protection.  

> [!IMPORTANT]  
>  Se você gerencia o endpoint protection para computadores Windows 10, configure o Configuration Manager para atualizar e distribuir as definições de malware para o Windows Defender. O Windows Defender está incluído no Windows 10, mas o SCEPInstall ainda deve ser instalado e as configurações de cliente personalizadas para o Endpoint Protection (**Etapa 5** abaixo) ainda são necessárias.  

|Etapas|Detalhes|  
|-----------|-------------|  
|**Etapa 1:** Criar uma função do sistema de sites do ponto do Endpoint Protection.|A função do sistema de sites do ponto do Endpoint Protection deve ser instalada antes que você possa usar o Endpoint Protection. Ela deve estar instalada em apenas um servidor do sistema de sites e deve estar instalada no topo da hierarquia em um site de administração central ou em um site primário autônomo. Consulte a [Etapa 1: Criar uma função do sistema de sites do ponto do Endpoint Protection](../../protect/deploy-use/configure-endpoint-protection.md).|  
|**Etapa 2:** Configurar alertas para o Endpoint Protection.|Os alertas informam o administrador quando eventos específicos ocorrem, como no caso de uma infecção por malware. Os alertas são exibidos no nó **Alertas** do espaço de trabalho **Monitoramento** ou, como opção, podem ser enviados por email para usuários especificados. Consulte [Etapa 2: Configurar alertas para o Endpoint Protection](../../protect/deploy-use/configure-endpoint-protection.md).|  
|**Etapa 3:** Configurar atualizações de definição para o Endpoint Protection.|O Endpoint Protection pode ser configurado para usar várias origens para baixar atualizações de definições. Consulte [Etapa 3: Configurar atualizações de definição para o Endpoint Protection](../../protect/deploy-use/configure-endpoint-protection.md).|  
|**Etapa 4:** Configurar a política antimalware padrão e criar políticas antimalware personalizadas.|A política antimalware padrão é aplicada quando o cliente do Endpoint Protection está instalado. As políticas personalizadas que você implantou são aplicadas por padrão até 60 minutos após a implantação do cliente. Verifique se você configurou as políticas antimalware antes de implantar o cliente do Endpoint Protection. Consulte [Como criar e implantar políticas antimalware para o Endpoint Protection no System Center Configuration Manager](../../protect/deploy-use/endpoint-antimalware-policies.md).|  
|**Etapa 5:** Definir configurações personalizadas do cliente para o Endpoint Protection.|Use configurações personalizadas do cliente para definir as configurações do Endpoint Protection para coleções de computadores em sua hierarquia.<br /><br /> Observações: não defina as configurações do cliente padrão do Endpoint Protection, a menos que tenha certeza de que deseja aplicá-las a todos os computadores na hierarquia. Consulte a [Etapa 5: Definir configurações personalizadas do cliente para o Endpoint Protection](../../protect/deploy-use/configure-endpoint-protection.md).|  



<!--HONumber=Dec16_HO3-->


