---
title: Configurando o Endpoint Protection | Microsoft Docs
description: "Saiba como gerenciar a segurança e malware em computadores cliente no System Center Configuration Manager."
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
ms.sourcegitcommit: bff083fe279cd6b36a58305a5f16051ea241151e
ms.openlocfilehash: 3678fd1e2ba70ad1cc03a3e0ca294901fae96255


---
# <a name="configuring-endpoint-protection-in-system-center-configuration-manager"></a>Configurando o Endpoint Protection no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Para poder usar o Endpoint Protection para gerenciar a segurança e malware em computadores cliente do Configuration Manager, configure-o usando este tópico.  

## <a name="how-to-configure-endpoint-protection-in-configuration-manager"></a>Como configurar o Endpoint Protection no Configuration Manager  
 O Endpoint Protection no Configuration Manager tem dependências dentro e fora do produto.  

### <a name="configure-endpoint-protection-in-configuration-manager"></a>Configurar o Endpoint Protection no Configuration Manager  
Há cinco etapas para configurar o Endpoint Protection

|Etapa|Detalhes|
|---|----|
|Etapa 1|[Criar uma função do sistema de sites do ponto do Endpoint Protection](endpoint-protection-site-role.md) ‑ Instale a função do sistema de sites do ponto do Endpoint Protection |
|Etapa 2|[Configurar alertas para o Endpoint Protection](endpoint-configure-alerts.md) ‑ Configurar alertas do Endpoint Protection para notificar os administradores quando eventos de segurança específicos na sua hierarquia ocorrerem|
|Etapa 3 | [Configurar fontes de atualização de definição para clientes do Endpoint Protection](endpoint-definition-updates.md) ‑ Escolha um dos métodos disponíveis para manter definições antimalware atualizadas nos computadores cliente|
|Etapa 4|[Configurar a política antimalware padrão e criar políticas antimalware personalizadas](endpoint-antimalware-policies.md) ‑ A política antimalware padrão é aplicada quando o cliente do Endpoint Protection está instalado, enquanto as políticas personalizadas são aplicadas dentro de 60 minutos após a implantação do cliente|
|Etapa 5|[Definir configurações de cliente personalizado para Endpoint Protection](endpoint-protection-configure-client.md) ‑ Defina as configurações de cliente personalizadas para o Endpoint Protection implantar as coleções de computadores|

> [!IMPORTANT]  
>  Se você gerencia o endpoint protection para computadores Windows 10, configure o Configuration Manager para atualizar e distribuir as definições de malware para o Windows Defender. O Windows Defender está incluído no Windows 10, mas o SCEPInstall ainda deve ser instalado e as configurações de cliente personalizadas para o Endpoint Protection (Etapa 5) ainda são necessárias.  



<!--HONumber=Dec16_HO3-->


